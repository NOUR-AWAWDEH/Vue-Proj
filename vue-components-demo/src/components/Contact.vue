<template>
    <div class="bg-info rounded p-4 m-1">
        <div class="row">
            <div class="col-12">
                <h3>Name : {{ name }}</h3>
                <p>Email : {{ email }}</p>
                <p>Phone : {{ phone }}</p>
                <p>Owner : {{ ownerName }}</p>
            </div>
            <div class="col-3">
                <button 
                @click="toggleFavorite()"
                :class="[isFavorite ? 'btn btn-warning' : 'btn btn-success']" >
                    {{ isFavorite ? "Remove from": "Add to" }} Favorite
                </button>

                  <button 
                        type="delete" 
                        class="btn btn-danger w-100"
                        @click="onDeleteContact()">Delete Contact
                 </button>
            </div> 
        </div>    
        <span class="float-end small" v-if="ownerName != ''">
             *this contact info belongs to {{ ownerName }}
        </span>
    </div>
</template>
<script setup>

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    phone: {
        type: String,
        required: false,
    },
    ownerName: {
        type: String,
        required: true
    },
    isFavorite: {
        type: Boolean,
        default: false
    }
});

function toggleFavorite() {
    emit("update-favorite", props.isFavorite);
};

function onDeleteContact() {
    emit("delete-contact", {
        name: props.name,
        email: props.email,
        phone: props.phone,
        ownerName: props.ownerName,
        isFavorite: props.isFavorite,
    });
}


const emit = defineEmits(['update-favorite', 'delete-contact']);
</script>