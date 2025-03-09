<script setup lang="ts">
defineProps<{
  content: string
  active: boolean
}>()
</script>

<template>
  <div class="square" :class="{ active: active }" @click="$emit('fill')">
    {{ content }}
  </div>
</template>

<style>
.square {
  border-radius: 0.5rem;
  margin: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  transition: all 500ms;
  border: 0.25rem solid black;
}
.square.active {
  border: 0.25rem solid hotpink;
}
</style>
