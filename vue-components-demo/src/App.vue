<template>
  <div class="bg-black text pt-3" :style="{ height: '100vh' }">
    <h1 class="text-center text-success">ContactOPedia</h1>
    <div class="container">
      <div class="row text-white p-2 mb-2">
        <div class="col-6">
          Owner Name : <input type="text" v-model="ownerName" />
        </div>
        <div class="col-6 text-start">
          Max Lucky Number : <input type="number" v-model.number="maxNumber" />
        </div>
      </div>
      <br /><br />
      <AddContact
      :onAddContact="onAddContact"></AddContact
      >>
      <div class="row">
        <div class="col-12" v-for="contact in contacts" :key="contact.name">
          <Contact
            :name="contact.name"
            :email="contact.email"
            :phone="contact.phone"
            :ownerName="contact.ownerName"
            :isFavorite="contact.isFavorite"
            @update-favorite="contact.isFavorite = onUpdateFavorite(contact.isFavorite)"
            @delete-contact="onDeleteContact"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, provide } from "vue";
import Contact from "./components/Contact.vue";
import AddContact from "./components/AddContact.vue";

const ownerName = ref("Nour Aldeen");
const contacts = reactive([]);
const maxNumber = ref(100);
provide("maxLuckyNumber", maxNumber);

function onUpdateFavorite(isFavoriteFromChildComponent) {
  return !isFavoriteFromChildComponent;
}

function validateContact(contact) {
  if (!contact.name || !contact.email || !contact.phone) {
    alert("Please fill all fields");
    return false;
  } else {
    return true;
  }
}

function onAddContact(contact) {
  validateContact(contact);
  if (!validateContact(contact)) {
    return;
  } else {
    contact.ownerName = ownerName.value;
    contact.isFavorite = false;
    contacts.push(contact);
  }
}

function onDeleteContact(contact) {
  const index = contacts.findIndex(
    (c) =>
      c.name === contact.name &&
      c.email === contact.email &&
      c.phone === contact.phone
  );
  if (index > -1) {
    contacts.splice(index, 1);
  }
}
</script>

<style></style>
