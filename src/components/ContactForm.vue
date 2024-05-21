<template>
  <form @submit.prevent="submitForm">
    <label for="name">Nom/Prénom:</label>
    <input type="text" id="name" v-model="name" required />

    <label for="subject">Objet:</label>
    <input type="text" id="subject" v-model="subject" required />

    <label for="message">Message:</label>
    <textarea id="message" v-model="message" required></textarea>

    <button type="submit">Envoyer</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      subject: "",
      message: "",
    };
  },
  methods: {
    submitForm() {
      const mailtoLink = `mailto:${process.env.VUE_APP_CONTACT_EMAIL}?subject=${this.subject}&body=Nom/Prénom: ${this.name}%0D%0A${this.message}`;
      window.location.href = mailtoLink;
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
label {
  margin-top: 1rem;
}
input,
textarea {
  margin-top: 0.5rem;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #333;
  color: #fff;
  cursor: pointer;
}
</style>
