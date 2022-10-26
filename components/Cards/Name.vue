<script setup lang="ts">
interface NameProps {
  index: number,
  name: string
}
const props = defineProps<NameProps>()
const emit = defineEmits(['remove'])
const removeName = () => emit('remove', props.index)
</script>

<template>
  <div class="card">
    <div @click="removeName" id="close">&times;</div>
    <h4>{{ name }}</h4>
  </div>
</template>

<style scoped>
.card {
  background: slateblue;
  width: 30%;
  color: white;
  border-radius: 1rem;
  padding: .1rem;
  margin-right: .5rem;
  margin-bottom: 1rem;
  position: relative;
}

#close {
  float: right;
  position: relative;
  top: -.1rem;
  right: .2rem;
  cursor: pointer;
  color: white;
}
</style>