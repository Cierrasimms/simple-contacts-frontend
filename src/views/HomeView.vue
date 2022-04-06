<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id"></div>
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
    <div v-for="contact in contacts" v-bind:key="contact.id">
      <h2>{{ contact.first_name }}</h2>
      <h2>{{ contact.last_name }}</h2>

      <!-- <p>First name: {{ contact.first_name }}</p>
      <p>Last name: {{ contact.last }}</p>
      <p>Email: {{ contact.email }}</p>
      <p>Phone number: {{ contact.phone_number }}</p> -->
      <button v-on:click="showContacts(contact)">More Info</button>
    </div>
    <dialog id="contact-details">
      <form method="dialog">
        <h1>Contact Info</h1>
        <p>First name: {{ currentContact.first_name }}</p>
        <p>Last name: {{ currentContact.last_name }}</p>
        <p>Email: {{ currentContact.email }}</p>
        <p>Phone number: {{ currentContact.phone_number }}</p>
        <button>Close</button>
      </form>
    </dialog>
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
      currentContact: {},
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
    showContacts(contact) {
      this.currentContact = contact;
      document.querySelector("#contact-details").showModal();
    },
  },
};
</script>

<style></style>
