<script setup>
import { ref } from 'vue';

const props = defineProps(['id', 'top', 'left', 'width', 'height']);

const id = props.id;
const top = ref(props.top);
const left = ref(props.left);
const width = ref(props.width);
const height = ref(props.height);
const windowElement = ref(null);

let dragStartX;
let dragStartY

function dragStart(e) {
  // Save starting mouse cursor position for calculations
  dragStartX = e.clientX;
  dragStartY = e.clientY;

  windowElement.value.classList.add('hide-draggable');
}

function dragEnd(e) {
  e.preventDefault();

  if (!windowElement.value) {
    // This drag resulted in the window being closed, so nothing to do
    return;
  }

  // Calculate the delta
  const deltaX = dragStartX - e.clientX;
  const deltaY = dragStartY - e.clientY;

  // Modify the window DOM properties
  windowElement.value.classList.remove('hide-draggable');
  top.value = top.value - deltaY;
  left.value = left.value - deltaX;

  // Make sure the window stays in bounds
  if (top.value < 0) {
    top.value = 0;
  } else if (top.value + height.value > window.innerHeight) {
    top.value = window.innerHeight - height.value;
  }

  if (left.value < 0) {
    left.value = 0
  } else if (left.value + width.value > window.innerWidth) {
    left.value = window.innerWidth - width.value;
  }
}
</script>

<template>
  <div draggable="true" class="window" @dragstart="dragStart" @dragend="dragEnd"
    :style="{ top: `${top}px`, left: `${left}px`, width: `${width}px`, height: `${height}px` }" ref="windowElement">
    <div class="area-label">
      <div class="window-close">
        <div class="closeButton" @click="$emit('close')">
        </div>
      </div>
      <div class="window-title">
        <slot name="header"></slot>
      </div>
    </div>
    <div class="window-content">
      <slot name="content"></slot>
    </div>
  </div>
</template>

<style>
.area-label {
  cursor: move;
  background-color: black;
  padding: 5px;
  color: white;
  float: left;
  display: flex;
  width: auto;
  flex-direction: row;
}

.area-label::after {
  content: "";
  clear: both;
}

.drag-icon {
  width: .9em;
  height: .9em;
  fill: white;
}

.window {
  background-color: white;
  position: fixed;
  flex: 1 1 auto;
  border: 2px solid black;
  display: flex;
  flex-direction: column;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  box-shadow: 10px 10px 39px -22px rgba(0, 0, 0, 0.75);
}

.window-content {
  overflow-y: auto;
  padding-top: 5px;
  clear: both;
  padding-left: 10px;
  padding-right: 10px;
  padding-bottom: 10px;
}

.hide-draggable {
  transition: 0.01s;
  transform: translateX(-9999px);
}

.window-title {
  flex: 1;
}

.window-close {
  flex: 0;
  padding-right: 5px;
}

.closeButton {
  cursor: pointer;
  display: block;
  width: .9em;
  height: .9em;
  background-color: rgb(255, 0, 0);
  border-radius: 10px;
}

.closeButton:hover {
  background-color: rgb(200, 0, 0);
}
</style>