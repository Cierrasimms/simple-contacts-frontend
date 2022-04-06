<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id">
      <h2>{{ contact.first_name }}</h2>
      <h2>{{ contact.last_name }}</h2>
      <h2>{{ contact.email }}</h2>
      <h2>{{ contact.phone_number }}</h2>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Meep",
      contacts: [],
    };
  },
  created: function () {
    this.indexContacts();
  },
  methods: {
    indexContacts() {
      axios.get("/contacts").then((response) => {
        console.log(response.data);
        this.contacts = response.data;
      });
    },
  },
};
</script>

<style></style>
