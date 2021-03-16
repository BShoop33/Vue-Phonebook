<template>
  <div>
    <h3 class="teal--text">New Contact</h3>
    <v-form @submit.prevent="handleSubmit" ref="contactForm">
      <v-text-field
        outlined
        label="First Name"
        v-model="form.firstName"
        :rules="validators.firstName"
        ref="firstNameInput"
      />
      <v-text-field
        outlined
        label="Last Name"
        v-model="form.lastName"
        :rules="validators.lastName"
        ref="lastNameInput"
      />
      <v-text-field
        outlined
        label="Phone"
        v-model="form.phone"
        :rules="validators.phone"
        ref="phoneInput"
      />
      <v-select
        outlined
        label="Phone Type"
        :items="phoneTypeOptions"
        v-model="form.type"
        ref="typeInput"
      />
      <v-text-field
        outlined
        label="Email"
        v-model="form.email"
        ref="emailInput"
      />
      <v-btn type="submit" color="teal">Submit</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: "",
      },
      phoneTypeOptions: ["Home", "Cell", "Office"],
      validators: {
        firstName: [
          //validates that the first name cannot be blank and if it is then returns the message that "Contact first name is required"
          (val) => !!val || "Contact first name is required",
          //validates that the first name must be shorter than 25 characters and if it is not then returns the message that "Contact first name is required"
          (val) =>
            val.length < 25 || "First name must be fewer than 25 characters",
        ],
        lastName: [
          //validates that the last name must be shorter than 25 characters and if it is not then returns the message that "Contact last name is required"
          (val) =>
            val.length < 25 || "Last name must be fewer than 25 characters",
        ],
        phone: [
          (val) => !!val || "Contact phone is required",
          (val) =>
            (val.length < 11 && val.length > 9) ||
            "Phone must be 10 numbers in length",
        ],
      },
    };
  },

  methods: {
    handleSubmit() {
      const isValid = this.$refs.contactForm.validate();
      if (!isValid) {
        return;
      }

      this.$emit("contact-submit", this.form);
      this.$refs.contactForm.resetValidation();
      this.$refs.firstNameInput.value = "";
      this.$refs.lastNameInput.value = "";
      this.$refs.phoneInput.value = "";
      this.$refs.typeInput.value = "";
      this.$refs.emailInput.value = "";
    },
  },
};
</script>

<style>
</style>