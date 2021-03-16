<template>
  <div>
    <contacts-table :contacts="contacts" />
    <contact-form @contact-submit="addContact" />
  </div>
</template>

<script>
import ContactForm from "./ContactForm.vue";
import ContactsTable from "./ContactsTable.vue";

export default {
  components: { ContactForm, ContactsTable },

  data() {
    return {
      contacts: [],
    };
  },

  methods: {
    addContact(newContact) {
      this.contacts.push(newContact);
      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    },
  },
};
</script>

<style></style>