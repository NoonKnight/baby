<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data"

interface OptionProps {
  index: number,
  option: {
    title: string
    category: string
    buttons: Gender[] | Popularity[] | Length[]
  },
  options: {
    gender: Gender
    popularity: Popularity
    length: Length
  },
}
const props = defineProps<OptionProps>()
function getButtonClasses(label, index: number) {
  const classes = []
  if (props.options[props.option.category] === label) {
    classes.push('option-active')
  }
  if (index === 0) {
    classes.push('option-left')
  }
  if (index === props.option.buttons.length - 1) {
    classes.push('option-right')
  }
  return classes.join(' ')
}
</script>

<template>
  <div class="option-container">
    <h4>{{ `${index + 1}) ${option.title}` }}</h4>
    <div class="option-buttons">
      <button v-for="(label, index) in option.buttons" :key="label" @click="options[option.category] = label"
        class="option" :class="getButtonClasses(label, index)">{{ label }}</button>
    </div>
  </div>
</template>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}

.option {
  font-size: 1rem;
  color: black;
  outline: .2rem solid salmon;
  border: 0;
  padding: .7rem;
  cursor: pointer;
  align-items: center;
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
  flex: 1;
}

.option-buttons {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background: salmon;
  color: white;
  font-weight: bold;
}
</style>