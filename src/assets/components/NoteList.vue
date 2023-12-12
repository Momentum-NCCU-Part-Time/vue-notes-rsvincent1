<template>

    <div class="note-list" >

    <div v-for="item in items" :key="item.id">
     <span class="titleNote"> {{ item.title }} </span>
     <span class="bodyNote"> {{ item.body }}</span>
     <span class="updateTime">{{ item.updatedAt }}</span>
      <button @click.prevent="deleteNote(item.id)">Delete</button>
      <button @click.prevent="editNote(item.id)">Edit</button>
    </div>
  </div>
 
</template>

<script setup>
// import NoteList from "./assets/components/NoteList.vue"

import { ref } from "vue";

let items = ref([]);

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
        displayNote();
      }

      
    );
};
</script>
