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
          <input type="checkbox" class="checkbox" v-model="entry.complete">
          <span :class="{ complete: entry.complete }">{{ entry.text }}</span>
          <button id="delete" @click="deleteEntry(entry)">X</button><br/><br/>
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
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto 1fr;
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
  justify-content: center;
  padding-left: 32%;
}

.content {
  grid-area: content;
  background-color: rgb(150, 102, 212);
  border-radius: 15%;
  height: 86vh;
  margin-top: 2%;
  padding-left: 8%;
  flex: 1 0 auto;
  flex-wrap: wrap;
  box-shadow: 4px 3px;

}

.new-entry {
  grid-area: content-top;
  width: 40%;
  height: 110%;
  align-self: center;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  flex: 1 3 auto
}

ul {
  padding-left: 0px;
}

li {
  list-style: none;
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
}

#hide-completed {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  margin-left: 10%;
  flex: 1 1 auto;
}

.complete {
  text-decoration: line-through;
}



</style>
