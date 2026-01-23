<script setup></script>

<template>
  <div class="layout">
    <h1>To Do List</h1>
    <div class="content-top">
    <button class="new-entry">New Entry</button>
    </div>
    <div class="content">
      <ul>
        <li><input type="checkbox" class="checkbox"><span class="list-item">List-element text.</span><input type="button" value="-" id="delete"></input><br/><br/></li>
        <!-- Use computed values for button value to have an image rather than text -->
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
}

.content {
  grid-area: content;
  outline: solid 1px red;
}

.new-entry {
  grid-area: content-top;
  width: 40%;
  height: 110%;
}

li {
  list-style: none;
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
}



</style>
