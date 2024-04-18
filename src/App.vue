<script setup>
import Window from './components/Window.vue'

// This allows windows to be moved without animating a "ghost"
// that slides back to the window's original location
function noGhosts(e) {
  e.preventDefault();
}

function dropped(e) {
  console.log('Window was moved: ', e);
}

function closeWindow() {
  console.log('Window close button was clicked');
}
</script>

<template>
  <div id="wrapper" @dragover="noGhosts" @drop="dropped">
    <Window id="test-window" :top="100" :left="100" :width="400" :height="400" @close="closeWindow()">
      <template #header>
        Test Window
      </template>
      <template #content>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore
        magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
        consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
        pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est
        laborum.
      </template>
    </Window>
  </div>
</template>

<style scoped>
#wrapper {
  position: relative;
  height: 100%;
  overflow: hidden;
}

#wrapper {
  background: white;
  background-image: radial-gradient(gray 1px, transparent 0);
  background-size: 20px 20px;
  background-position: -19px -19px;
}
</style>