<template>

    <div class="note-list" >

    <div v-for="item in items" :key="item.id">
     <span class="titleNote"> {{ item.title }} </span>
     <span class="bodyNote"> {{ item.body }}</span>
     <span class="updateTime">{{ item.updatedAt }}</span>
      <!-- <button @click.prevent="deleteNote(item.id)">Delete</button>
      <button @click.prevent="editNote(item.id)">Edit</button> -->
    </div>
  </div>
 
</template>

<script setup>
// import DeleteNote from "./assets/components/DeleteNote.vue";
// import EditNote from "./assets/components/EditNote.vue";
import EditNote from "./EditNote.vue";
import DeleteNote from "./DeleteNote.vue";
import { ref } from "vue";

// let items = ref([]);
const url = "http://localhost:3000/notes/"

let items = ref([]);
const newNote = ref("");
const noteTitle = ref("");
const noteBody = ref("");



const displayNote = () => {
  fetch(url, {
    method: "GET",
    headers: { "Content-Type": "application/json" },
  })
    .then((res) => res.json())
    .then(
      (data) => {
        
        items.value = data;
       
      }

    );
};
displayNote();
const saveNote = (note) => {
  const { title, body } = note;
  fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      title: noteTitle.value,
      body: noteBody.value,
      updatedAt: new Date()
    }),
  })
    .then((res) => res.json())

  items.value.push({ title: noteTitle.value, body: noteBody.value,  updatedAt: new Date(toLocaleString())});
  newNote.value = "";
  {
    {
      newNote;
    }
  }
};

displayNote();

</script>
