<template>
  <section :data-slide="slide.id"
    :data-active="state"
    :data-has-caption='hasCaption'
    @dblclick.prevent="$emit('openAtSlide');" >

    <component :data-slide-layout="getLayout"
      :style="style"
      :slide="slide"
      :meta="meta"
      :is="`${getLayout}-slide`" />

    <slide-caption v-if="hasCaption"
      :caption='getCaption'
      :tags='getTags(slide.data.tags)' />
  </section>
</template>

<script>
  import ContactSlide from '~/components/slide/ContactSlide.vue';
  import DefaultSlide from '~/components/slide/DefaultSlide.vue';
  import ImageSlide from '~/components/slide/ImageSlide.vue';
  import SlideCaption from '~/components/utility/SlideCaption.vue';

  export default {
    components: {
      ContactSlide,
      ImageSlide,
      DefaultSlide,
      SlideCaption,
    },
    props: {
      slide: {
        type: Object,
        required: true
      },
      meta: {
        type: Object,
        required: true
      },
      state: {
        type: [String, Boolean],
        required: true,
      },
    },
    computed: {
      hasCaption() {
        return this.slide.data.caption || this.slide.data.tags ? true : false;
      },
      getCaption() {
        if (this.slide.data.demo) {
          let demoPath = this.slide.data.demo;

          if (!this.meta.demos[demoPath]) {
            demoPath = `/demos/${demoPath}`;

            const demoUrl = `${process.env.domain}${demoPath}`;
            let caption = this.slide.data.caption;
            let demoCaption = `Demo: [${demoUrl}](${demoPath})`;

            caption = caption ? caption + ' | ' : '';
            return  caption + demoCaption;
          }
        }

        return this.slide.data.caption;
      },
      getLayout() {
        let defaultLayout = this.slide.data.image ? 'image' : 'default';
        defaultLayout = this.slide.data.split ? 'split' : defaultLayout;
        defaultLayout = this.slide.data.demo ? 'demo' : defaultLayout;
        return this.slide.data.layout || this.meta.layout || defaultLayout;
      },
      style() {
        const style = this.slide.data.style || {};

        if (this.slide.data.image) {
          style['--image'] = `url('${this.slide.data.image}')`;
        }

        if ((this.getLayout === 'image') || (this.getLayout === 'demo')) {
          if (!style['align-self'] && !style['--align-self']) {
            style['--align-self'] = 'stretch';
          }
        }

        return style;
      },
    },
    methods: {
      getTags(tags) {
        const sort = (arr) => {
          return arr.concat().sort();
        }
        return tags ? sort(tags) : false;
      },
    },
  }
</script>

<style lang="scss">
[data-slide] {
  @include transition('move');
  background-color: color('slide');
  border-radius: size('corner');
  box-shadow: pattern('shadow');
  display: grid;
  grid-template: 'main' 1fr 'caption' auto / minmax(0, 1fr);
  overflow: auto;

  @include before('') {
    grid-area: 1 / 1 / -1 / -1;
    width: 0;
    height: 0;
    padding-bottom: var(--ratio, 0);
  }
}

[data-slide-layout] {
  align-self: var(--align-self, center);
  background-image: var(--image);
  background-repeat: no-repeat;
  background-size: var(--image-size, cover);
  background-position: var(--image-position, center);
  grid-area: main;
  position: relative;
  width: 100%;

  h2,
  [data-code='h2'] {
    font-size: size('xlarger');
  }

  h3,
  [data-code='h3'] {
    font-size: size('larger');
  }
}
</style>
