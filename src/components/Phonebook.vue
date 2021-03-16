<template>
  <contact-form />
</template>

<script>
import ContactForm from "./ContactForm.vue";

export default {
  components: { ContactForm },

  data() {
    return {
      contacts: [],
    };
  },
};
</script>

<style></style>