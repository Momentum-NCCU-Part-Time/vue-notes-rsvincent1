<template>
    <button @click.prevent="deleteNote">Delete</button>
  </template>
<script setup>
import { ref } from 'vue';
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
</script>