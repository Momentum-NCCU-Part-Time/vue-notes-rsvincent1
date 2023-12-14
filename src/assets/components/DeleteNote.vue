<template>
    <button @click.prevent="deleteNote">Delete</button>
  </template>
<script setup>
import { ref } from 'vue';
import NoteList from "@/assets/components/NoteList.vue"
const url = "http://localhost:3000/notes/"
let items = ref([]);
const props = 
defineProps
({items:Object})
// console.log(props.items)
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
          deleteNote();
          console.log(props.items)
          
        }
  
      );
  };
</script>