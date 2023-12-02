<script setup>
import { ref } from 'vue'

const noteList = ref([]); // noteList is a reactive variable
const isOverlayVisible = ref(false);
const noteText = ref("");

function getRandomColor() {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

// toggle overlay
const toggleOverlay = () => {
  isOverlayVisible.value = !isOverlayVisible.value;
  noteText.value = "";
}

const addNote = () => {
  noteList.value.push({
    id: noteList.value.length,
    textData: noteText.value,
    date: new Date().toLocaleDateString(),
    backgroundColor: getRandomColor()
  });
  toggleOverlay();
}
</script>

<template>
  <main>
    <div class="overlay" v-if="isOverlayVisible">
      <div class="modal">
        <div class="text-container">
          <button @click="toggleOverlay()">x</button>
          <textarea v-model="noteText" name="note" id="note" cols="30" rows="10"></textarea>
        </div>
        <button @click="addNote()">Save</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="toggleOverlay()">+</button>
      </header>
      <div class="cards-container">
        <div class="card" v-for="note in noteList" :key="note.id" :style="{ backgroundColor: note.backgroundColor }">
          <div class="main-text">{{ note.textData }}</div>
          <div class="date">{{ note.date }}</div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100%;
  width: 100%;
}

#note {
  width: 100%;
  font-size: 16px;
  font-weight: bold;
  border-radius: 10px;
  margin-top: 10px;
}

.modal {
  width: 500px;
  height: 300px;
  background-color: white;
  border-radius: 10px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.text-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: end;
  align-items: end;
}

h1 {
  font-size: 50px;
  font-weight: bold;
  margin: 10px;
}

.overlay {
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header button {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.container {
  max-width: 1000px;
  /* padding: 10px; */
  margin: 0 auto;
}

.card {
  width: 225px;
  background-color: #2c2c2c;
  border-radius: 10px;
  margin: 10px;
  padding: 10px 30px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: start;
}

.main-text {
  font-size: 16px;
  font-weight: bold;
  color: #242424;
}

.date {
  font-size: 12px;
  font-weight: bold;
  color: #242424;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}
</style>
