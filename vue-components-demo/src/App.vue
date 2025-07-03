<template>
    <div class="bg-info rounded p-4 m-1">
        <h2>Contacts List</h2>
        <input v-model="ownerName" />
    </div>
    <br/>
    <div class="bg-black rounded p-4 m-1">
        <AddContact 
            @add-contact="onAddContact"
            @remove-contact="onRemoveContact"></AddContact>>
    </div>
    
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
</template>

<script setup>

import {ref, reactive } from "vue";
import Contact from "./components/Contact.vue";
import AddContact from "./components/AddContact.vue";

const ownerName = ref("Nour Aldeen");
const contacts = reactive([]);
 

function onUpdateFavorite(isFavoriteFromChildComponent) {
    return !isFavoriteFromChildComponent;
}

function validateContact(contact){
    if (!contact.name || !contact.email || !contact.phone) {
        alert("Please fill all fields");
        return false;
    }else {
        return true;
    }
}

function onAddContact(contact) {
    validateContact(contact);
    if (!validateContact(contact)) {
        return;
    }else {
        contact.ownerName = ownerName.value;
        contact.isFavorite = false;
        contacts.push(contact);
    }
}

function onDeleteContact(contact) {
    const index = contacts.findIndex(c => c.name === contact.name && c.email === contact.email && c.phone === contact.phone);
    if (index > -1) {
        contacts.splice(index, 1);
    }
}

</script>

<style>
</style>