<template>
  <form data-part="contact-form"
    :action="`https://formspree.io/${slide.data.form.email}`"
    method="POST">

    <h4 class="form-header">Stay in touch…</h4>

    <input type="hidden"
      name="_next"
      :value="slide.data.form.next" />
    <input type="text"
      name="_gotcha"
      style="display:none" />

    <label for="contact-name"
      data-form-field="contact-name"
      data-field-state="required" >
      <span data-label="contact-name">Name</span>
      <input id="contact-name"
        name="contact-name"
        data-input="default"
        required="true"
        type="text"
        @focus="listen(false)"
        @blur="listen(true)" >
    </label>

    <label for="contact-email"
      data-form-field="contact-email"
      data-field-state="required" >
      <span data-label="contact-email">Email Address</span>
      <input id="contact-email"
        name="_replyto"
        data-input="default"
        required="true"
        type="email"
        @focus="listen(false)"
        @blur="listen(true)" />
    </label>

    <label for="contact-message"
      data-form-field="contact-message"
      data-field-state="required" >
      <span data-label="contact-message">Message</span>
      <textarea id="contact-message"
        name="contact-message"
        data-input="textarea"
        required="true"
        @focus="listen(false)"
        @blur="listen(true)" />
    </label>

    <div data-actions>
      <button-style type="submit"
        id="contact-submit"
        :content="slide.data.form.submit" />
    </div>
  </form>
</template>

<script>
  import ButtonStyle from '~/components/utility/ButtonStyle.vue';

  export default {
    components: {
      ButtonStyle,
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
    },
    methods: {
      listen(value) {
        this.meta.listen = value;
      }
    },
  }
</script>

<style lang="scss" scoped>
[data-part='contact-form'] {
  align-self: center;
  display: grid;
  grid-gap: size('half-shim');
  grid-template-columns: repeat(auto-fit, minmax(size('half-page'), 1fr));
  margin: 0 auto;
  max-width: size('wide');
  padding: size('gutter');
  text-align: left;
  width: 100%;
}

.form-header,
[data-form-field='contact-message'],
[data-actions] {
  grid-column: 1 / -1;
}

[data-form-field] {
  display: block;
}

[data-label] {
  display: block;
  font-size: size('xsmaller');
}

[data-input='default'],
[data-input='textarea'] {
  border: pattern('border');
  border-radius: size('corner');
  font-size: size('xsmall');
  padding: size('half-shim');
  transition: border-color 250ms ease;
  width: 100%;

  &:invalid {
    border-color: color('accent');
  }

  &:focus {
    border-color: color('action-hover');
    outline: 0;
  }
}

[data-input='textarea'] {
  min-height: size('double-gutter');
}

[data-actions] {
  text-align: right;
}
</style>
