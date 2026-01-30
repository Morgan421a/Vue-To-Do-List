<script setup>
import { ref, computed } from 'vue';

let id = 0
const hideCompleted = ref(false)
const entries = ref([
  { id: id++, text: "You Can Delete Me", complete: false } // Stores entries in an array, gives each entry and id key
])

function addEntry() {
  const newEntry = prompt("Enter a new task:");
  if (newEntry != null) { // only executes if newEntry not empty
    entries.value.push({ id: id++, text: newEntry, complete: false })
  }
}

function deleteEntry(entry) {
  entries.value = entries.value.filter((t) => t !== entry)
}

const completedTasks = computed(() => {
  return hideCompleted.value
  ? entries.value.filter((t) => !t.complete)
  : entries.value
})

</script>

<template>
  <div class="layout">
    <h1>To Do List</h1>
    <div class="content-top">
    <button class="new-entry" @click="addEntry">New Entry</button>
    <span id="hide-completed"><input type="checkbox" @click="hideCompleted = !hideCompleted">Hide completed tasks</span>
    </div>
    <div class="content">
      <ul>
        <li v-for="entry in completedTasks" :key="entry.id">
          <span class="row">

            <input type="checkbox" class="checkbox" v-model="entry.complete">
            <span :class="{ complete: entry.complete }">{{ entry.text }}</span>
            <button id="delete" @click="deleteEntry(entry)">X</button>

          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>

html, body {
  margin: 0;
  padding: 0;
}

</style>

<style scoped>

.layout {
  height: 100vh;
  display: grid;
  grid-template-areas:
      "topbar  topbar  topbar"
      "left-blank content-top right-blank"
      "left-blank content  right-blank";
  grid-template-rows: auto auto 1fr;
  grid-template-columns: 1fr minmax(0, 600px) 1fr;
  gap: 0rem;
  background-image: linear-gradient(to top, purple, white);
}

h1 {
  text-align:center;
  grid-area: topbar;
}

.content-top {
  grid-area: content-top;
  display: flex;
  align-items: center;
  padding-left: 30%;
}

.content {
  grid-area: content;
  background-color: rgb(150, 102, 212);
  border-radius: 15%;
  height: 86vh;
  margin-top: 2%;
  padding-left: 8%;
  box-shadow: 4px 3px;
  display: flex;
  flex-wrap: wrap;
  overflow: auto;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.content::-webkit-scrollbar {
  display: none;
}

.new-entry {
  grid-area: content-top;
  height: 110%;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  flex: 0 0 auto;
  border-radius: 16px;
}

ul {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  padding-left: 0px;
  min-width: 0;
  max-width: 90%;
}

li {
  list-style: none;
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
}

li span, #delete {
  overflow-wrap: break-word;
  word-break: break-word;
  min-width: 0;
}

#hide-completed {
  display: inline-flex;
  box-sizing: border-box;
  margin-left: 10%;
  flex: 1 1 auto;
}

.complete {
  text-decoration: line-through;
}

#delete {
  display: flex;
  border-radius: 50%;
  flex: 1 0 auto;
}

button,
input {
  cursor: pointer;
}

.row {
  display: flex;
  align-items: center;  /* Wraps li content ensuring all buttons and inputs don't become disconnected  */
  gap: 0.2rem;
  min-width: 0;
}


</style>
