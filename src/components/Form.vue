<template>
  <div :class="$style['form-wrapper']">
    <FormInputUrl
      :url="url"
      :error="errors.url"
      @urlChange="urlChangeHandler"
      @submitForm="submitHandler"
    />
    <FormInputText
      :text="text"
      :error="errors.text"
      @textChange="textChangeHandler"
    />
  </div>
</template>

<script>
import FormInputUrl from "./FormInputUrl";
import FormInputText from "./FormInputText";

export default {
  name: "Form",
  components: {
    FormInputUrl,
    FormInputText,
  },
  data() {
    return {
      url: "",
      text: "",
      errors: {
        url: false,
        text: false,
      },
    };
  },
  methods: {
    urlChangeHandler(newUrl) {
      this.url = newUrl;
      this.errors.url = false;
    },
    textChangeHandler(newText) {
      this.text = newText;
      this.errors.text = false;
    },
    submitHandler() {
      if (this.url.trim().length === 0) {
        this.errors.url = true;

        return;
      }

      if (this.text.trim().length === 0) {
        this.errors.text = true;

        return;
      }

      this.$emit("search", this.url, this.text);
    },
  },
};
</script>

<style module>
.form-wrapper {
  width: 100%;
}
</style>