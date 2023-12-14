
<template>
  <div class="container">
    <h1>Vue Notes</h1>

    <form class="add-note-form" @submit.prevent="saveNote">
      <input class="inputTitle" v-model.trim="noteTitle" placeholder="Title" type="text" />
      <input class="inputBody" v-model.trim="noteBody"  placeholder="Body" type="text" />
      <button class="saveButton">Save note</button>
    </form>
  
    <NoteList :items="items" />
    </div>
  </template>
<style scoped> </style>


<script setup>
import NoteList from "./assets/components/NoteList.vue"
import { ref } from "vue";
let items = ref([]);
const newNote = ref("");
const noteTitle = ref("");
const noteBody = ref("");


// const url = "http://localhost:3000/notes/"

// let items = ref([]);
// const newNote = ref("");
// const noteTitle = ref("");
// const noteBody = ref("");



// const displayNote = () => {
//   fetch(url, {
//     method: "GET",
//     headers: { "Content-Type": "application/json" },
//   })
//     .then((res) => res.json())
//     .then(
//       (data) => {
        
//         items.value = data;
       
//       }

//     );
// };

// const saveNote = (note) => {
//   const { title, body } = note;
//   fetch(url, {
//     method: "POST",
//     headers: { "Content-Type": "application/json" },
//     body: JSON.stringify({
//       title: noteTitle.value,
//       body: noteBody.value,
//       updatedAt: new Date()
//     }),
//   })
//     .then((res) => res.json())

//   items.value.push({ title: noteTitle.value, body: noteBody.value,  updatedAt: new Date()});
//   newNote.value = "";
//   {
//     {
//       newNote;
//     }
//   }
// };

// // displayNote();

// const deleteNote = (id) => {
//   fetch(url + id, {
//     method: "DELETE",
//     headers: { "Content-Type": "application/json" },
//   })
//     .then((res) => res.json())
//     .then(
//       (data) => {
        
//         items.value = data;
//         displayNote();
//       }

//     );
// };

// const editNote = (id) => {
//   fetch(url + id, {
//     method: "PATCH",
//     headers: { "Content-Type": "application/json" },
//     body: JSON.stringify({
//       title: noteTitle.value,
//       body: noteBody.value,
     
//     }),
//   })
//     .then((res) => res.json())
//     .then(
//       (data) => {
        
//         items.value = data;
//         // displayNote();
//       }

      
//     );
// };
// displayNote();



</script>