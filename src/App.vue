<script setup>
import NoteList from "./assets/components/NoteList.vue"

import { ref } from "vue";
let items = ref([]);
const noteTitle = ref("");
const noteBody = ref("");


</script>
<template>
  <div class="container">
    <h1>Vue Notes</h1>

    <form class="add-note-form" @submit.prevent="saveNote">
      <input class="inputTitle" v-model.trim="noteTitle" placeholder="Title" type="text" />
      <input class="inputBody" v-model.trim="noteBody"  placeholder="Body" type="text" />
      <button class="saveButton">Save note</button>
    </form>
    <NoteList :items="items"
    @deleteNote=""
    @editNote=""/>
    </div>
  </template>
<style scoped> </style>

