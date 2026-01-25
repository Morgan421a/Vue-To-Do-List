<script setup>
import { ref } from 'vue';

let id = 0

const entries = ref([
  { id: id++, text: "You Can Delete Me", complete: true } // Stores entries in an array, gives each entry and id key
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

</script>

<template>
  <div class="layout">
    <h1>To Do List</h1>
    <div class="content-top">
    <button class="new-entry" @click="addEntry">New Entry</button>
    <span id="hide-completed"><input type="checkbox">Hide completed tasks</span>
    </div>
    <div class="content">
      <ul>
        <li v-for="entry in entries" :key="entry.id">
          <input type="checkbox" class="checkbox">
          <span>{{ entry.text }}</span>
          <button id="delete" @click="deleteEntry(entry)">X</button><br/><br/>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.layout {
  display: grid;
  grid-template-areas:
      "topbar  topbar  topbar"
      "left-blank content-top right-blank"
      "left-blank content  right-blank"
      "left-footer content  right-footer";
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
  outline: solid 1px red;
  padding-left: 32%;
}

.content {
  grid-area: content;
  outline: solid 1px red;
  background-color: rgb(150, 102, 212);
  border-radius: 15%;
  height: 87vh;
  margin-top: 2%;
  padding-left: 8%;
  flex: 1 0 auto;
  flex-wrap: wrap;
}

.new-entry {
  grid-area: content-top;
  width: 40%;
  height: 110%;
  align-self: center;
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
  outline: 1px solid blueviolet;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  margin-left: 10%;
}




</style>
