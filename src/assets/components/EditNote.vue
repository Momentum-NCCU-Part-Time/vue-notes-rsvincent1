<template>
    <button @click.prevent="editNote">Edit</button>
  </template>

<script setup>
import { ref } from 'vue';
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