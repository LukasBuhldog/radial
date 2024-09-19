<script setup>
import { ref } from 'vue';

// mouse position constants
const mouseX = ref(0);
const mouseY = ref(0);
const isMenuShown = ref(false);

// Function to handle click and toggle the menu
function handleClick(event) {
  // If the menu is currently hidden, capture the mouse position and show the menu
  if (!isMenuShown.value) {
    mouseX.value = event.clientX;
    mouseY.value = event.clientY;
  }
  
  // Toggle the menu visibility
  isMenuShown.value = !isMenuShown.value;
}
</script>

<template>
  <!-- Div covers the whole screen and listens for click events -->
  <div @click="handleClick" id="wholeScreen">

    <!-- Four buttons arranged around the click point -->
    <div
      v-if="isMenuShown"
      v-for="(button, index) in buttons"
      :key="index"
      class="circle-button"
      :style="{
        top: mouseY + button.topOffset + 'px',
        left: mouseX + button.leftOffset + 'px',
      }"
    ></div>
  </div>
</template>

<script>
// Button positions around the click point
const buttons = [
  { topOffset: 75, leftOffset: -25 },   // Bottom
  { topOffset: -125, leftOffset: -25 }, // Top
  { topOffset: -25, leftOffset: 75 },   // Right
  { topOffset: -25, leftOffset: -125 }, // Left
];
</script>
