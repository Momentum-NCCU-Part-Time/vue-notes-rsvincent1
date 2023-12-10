<script setup>
import { ref } from "vue";

const url = "http://localhost:3000/notes/"

let items = ref([]);
const newNote = ref("");
const noteTitle = ref("");
const noteBody = ref("");



const displayNote = () => {
  fetch("http://localhost:3000/notes/", {
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

const saveNote = (note) => {
  const { title, body } = note;
  fetch("http://localhost:3000/notes/", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      title: noteTitle.value,
      body: noteBody.value,
     
    }),
  })
    .then((res) => res.json())
    .then(
      (data) => console.log(data)

    );


  items.value.push({ title: noteTitle.value, body: noteBody.value });
  newNote.value = "";
  {
    {
      newNote;
    }
  }
};

displayNote();

const deleteNote = (id) => {
  fetch(url + id, {
    method: "DELETE",
    headers: { "Content-Type": "application/json" },
  })
    .then((res) => res.json())
    .then(
      (data) => {
        
        items.value = data;
        displayNote();
      }

      // or whatever you need to do
    );
};

const editNote = (id) => {
  fetch(url + id, {
    method: "PATCH",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      title: noteTitle.value,
      body: noteBody.value,
     
    }),
  })
    .then((res) => res.json())
    .then(
      (data) => {
        
        items.value = data;
        console.log(data)
        displayNote();
      }

      
    );
};

</script>

<template>
  <div>
    <h1>Vue Notes</h1>

    <form class="add-note-form" @submit.prevent="saveNote">
      <input v-model.trim="noteTitle" type="text" />
      <input v-model.trim="noteBody" type="text" />
      <button>Save note</button>
    </form>
    <div v-for="item in items" :key="item.id">
      {{ item.title }}
      {{ item.body }}
      <button @click.prevent="deleteNote(item.id)">Delete</button>
      <button @click.prevent="editNote(item.id)">Edit</button>
    </div>
  </div>
 
</template>

<style scoped></style>