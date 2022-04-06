<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id">
      <h2>{{ contact.first_name }}</h2>
      <h2>{{ contact.last_name }}</h2>
      <h2>{{ contact.email }}</h2>
      <h2>{{ contact.phone_number }}</h2>
    </div>
    <div>
      <h1>New Contact</h1>
      First name:
      <input type="text" v-model="newContact.first_name" />
      Last name:
      <input type="text" v-model="newContact.last_name" />
      Email:
      <input type="text" v-model="newContact.email" />
      Phone number:
      <input type="text" v-model="newContact.phone_number" />
      <button v-on:click="createContacts()">Create New Contact</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Contacts",
      contacts: [],
      newContact: {},
    };
  },
  created: function () {
    this.indexContacts();
    this.createContacts();
  },
  methods: {
    indexContacts() {
      axios.get("/contacts").then((response) => {
        console.log(response.data);
        this.contacts = response.data;
      });
    },
    createContacts() {
      axios.post("/contacts", this.newContact).then((response) => {
        console.log(response.data);
        this.contacts.push(response.data);
        this.newContacts = {};
      });
    },
  },
};
</script>

<style></style>
