<script setup>
import { ref } from "vue";


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
        // console.log(data)
        items.value = data;
      }

      // or whatever you need to do
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

      // or whatever you need to do
    );
  // items.value.push({id:items.value.length +1, label: newNote })
  // newNote.value=""

  items.value.push({ title: noteTitle.value, body: noteBody.value });
  newNote.value = "";
  {
    {
      newNote;
    }
  }
};

displayNote();

const deleteNote = () => {
  fetch("http://localhost:3000/notes/", {
    method: "DELETE",
    headers: { "Content-Type": "application/json" },
  })
    .then((res) => res.json())
    .then(
      (data) => {
        // console.log(data)
        items.value = data;
      }

      // or whatever you need to do
    );
};

// function deleteNote(notes) {
//   items.value = items.value.filter((item) => item !== items);
// }

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
      <button @click="deleteNote(notes)">Delete</button>
    </div>
  </div>
</template>

<style scoped></style>
