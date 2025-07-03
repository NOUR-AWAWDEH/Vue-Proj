<template>
    <div class="container border rounded p-2">
        <div class="text-center text-white"> Add new Contact</div>
        <form @submit.prevent="addContact()">
            <div class="row">
                <div class="col-4">
                    <input  
                        type="text" 
                        class="form-control"
                        v-model="contact.name" 
                        placeholder="Name"  
                    />
                </div>
                <div class="col-4">
                    <input  
                        type="text" 
                        class="form-control"
                        v-model="contact.email" 
                        placeholder="Email"  
                    />
                </div>
                <div class="col-4">
                    <input  
                        type="text" 
                        class="form-control"
                        v-model="contact.phone"
                        @input="onlyNumbers($event)" 
                        placeholder="Phone"  
                    />
                </div>
                <div class="col-6 offset-3 p-2">
                    <button 
                        type="submit" 
                        class="btn btn-secondary w-100"
                        @click="onAddContact()">Add Contact</button>                     
                </div>
            </div>
        </form>

    </div>
</template>

<script setup>
import { reactive } from 'vue';

const contact = reactive({
    name: '',
    email: '',
    phone: '',
});

function addContact() {
    emit('add-contact', {
        name: contact.name,
        email: contact.email,
        phone: contact.phone,
    });

    // Reset the contact form
    resetContact();
}

function resetContact() {
    contact.name = '';
    contact.email = '';
    contact.phone = '';
}


const emit = defineEmits(['add-contact']);

function onlyNumbers(event) {
    event.target.value = event.target.value.replace(/[^0-9]/g, '');
}
</script>