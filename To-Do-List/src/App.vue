<script setup>

import { ref, computed } from 'vue';

let id = 0
const hideCompleted = ref(false)
const entries = ref([
  { id: id++, text: "Welcome, you Can Delete Me", complete: false } // Stores entries in an array, gives each entry and id key
])

function addEntry() {
  const newEntry = prompt("Enter a new task:");
  if (newEntry != null) { // only executes if newEntry not empty
    entries.value.push({ id: id++, text: newEntry, complete: false })
  }
}

function deleteEntry(entry) {
  entries.value = entries.value.filter((t) => t !== entry) // Replaces old array with updated version after removing deleted entry
}

const completedTasks = computed(() => {
  return hideCompleted.value
  ? entries.value.filter((t) => !t.complete)
  : entries.value
}
)

const getDate = ref(new Date())

const formattedDate = computed(() =>
  getDate.value.toLocaleDateString( { // Allows reactive Date
    day: "2-digit",
    month: "2-digit",
    year: "numeric"
  })
)

</script>

<template>

  <div class="layout">
    <h1>To Do List</h1>

    <div class="content-top">
      <button class="new-entry" @click="addEntry">New Entry</button>
      <label class="hide-completed">
       <span class="hide-tasks"><input type="checkbox" @click="hideCompleted = !hideCompleted">Hide completed tasks</span>
      </label>
    </div>

    <div class="content">
      <h3>{{ formattedDate }}</h3>

      <ul class="task-list">
        <li v-for="entry in completedTasks" :key="entry.id">
          <span class="row">
            <label class="task">
              <input type="checkbox" class="checkbox" v-model="entry.complete">
              <span :class="{ complete: entry.complete }">{{ entry.text }}</span>
            </label>

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
  font-family: "Roboto", sans-serif;
}

button,
input,
span {
  cursor: pointer;
}

</style>

<style scoped>

.layout {
  height: 100vh;
  display: grid;
  grid-template-areas:
      "topbar  topbar  topbar"
      "left-blank content-top right-blank"
      "left-blank content right-blank"
      "footer footer footer";
  grid-template-rows: auto auto 1fr;
  grid-template-columns: 1fr minmax(0, 600px) 1fr;
  gap: 0rem;
  background-color: aliceblue;
}

h1 {
  text-align:center;
  grid-area: topbar;
  color: #191950;
}

.content-top {
  grid-area: content-top;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  margin-top: 12px;
  margin-bottom: 28px;
}

.new-entry {
  grid-area: content-top;
  height: 130%;
  box-sizing: border-box;
  font-size: 16px;
  text-decoration: none;
  color: white;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  flex: 0 0 auto;
  border-radius: 16px;
  background-color: #4448c2;
  border: none;
}

.hide-tasks{
  border-radius: 8px;
  padding: 8px 12px;
}

.hide-tasks:hover {
  background: rgba(110, 70, 70, 0.13);
}

.content {
  grid-area: content;
  display: flex;
  flex-direction: column;
  background-color: #4448c2;
  color: aliceblue;
  border-radius: 10%;
  margin-top: 2%;
  padding-left: 8%;
  padding-top: 2%;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.12);
  background: linear-gradient(180deg, #4f56d8, #3f46c5);
  overflow: auto;
  -ms-overflow-style: none;
  scrollbar-width: none;
  max-height: 80vh;
}

.content::-webkit-scrollbar {
  display: none;
}

h3 {
  align-self: center;
  margin-top: 0;
  margin-right: 8%;
}

ul {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  padding-left: 0px;
  min-width: 0;
  max-width: 90%;
}

.row {
  display: flex;
  align-items: center;  /* Wraps li content ensuring all buttons and inputs don't become disconnected  */
  gap: 0.2rem;
  min-width: 0;
}

.complete {
  text-decoration: line-through;
  color: black;
  opacity: 0.5;
}

li {
  list-style: none;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 8px 12px;
  border-radius: 8px;
}

li:hover {
  background: rgba(255,255,255,0.08);
}

li span, #delete {
  overflow-wrap: break-word;
  word-break: break-word;
  min-width: 0;
}

#delete {
  display: flex;
  border-radius: 50%;
  vertical-align: middle;
  flex: 1 0 auto;
  background-color: rgb(243, 53, 53);
  color: aliceblue;
  border: none;
  text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
  opacity: 0.5;
}

#delete:hover {
  opacity: 1;
}

input {
  appearance: none;
  height: 15px;
  width: 15px;
  border-radius: 50%;
}

label input {
  border: solid 1px #191950;
  margin-top: 1px;
  vertical-align: middle;
}

input.checkbox {
  margin-right: 5px;
  vertical-align: middle;
  border: solid 1px aliceblue;
}

input:checked{
  background-color: black;
}

</style>
