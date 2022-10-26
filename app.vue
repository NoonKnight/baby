<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data"
interface OptionState {
  gender: Gender
  popularity: Popularity
  length: Length
}
const options = reactive<OptionState>({
  gender: Gender.NEUTRAL,
  popularity: Popularity.UNIQUE,
  length: Length.ALL,
})
const findNames = () => {
  foundNames.value = names
    .filter(name => name.gender === options.gender)
    .filter(name => name.popularity === options.popularity)
    .filter(name => {
      if (options.length === Length.ALL) return true
      return name.length === options.length
    })
    .map(name => name.name)
}
const foundNames = ref<string[]>([])
const optionsArray = [
  {
    title: 'Choose a gender',
    category: 'gender',
    buttons: [Gender.BOY, Gender.NEUTRAL, Gender.GIRL],
  },
  {
    title: 'Choose the popularity',
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: 'Choose a length',
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  },
]
const removeName = (index: number) => {
  const filteredNames = [...foundNames.value]
  filteredNames.splice(index, 1)
  foundNames.value = filteredNames
}
</script>

<template>
  <div class="container">
    <h1>Baby Names</h1>
    <p>Generate baby names</p>
    <div class="options-container">
      <Option
        v-for="(option, index) in optionsArray"
        :key="option.title"
        :index="index"
        :option="option"
        :options="options"
      />
      <button @click="findNames" class="primary">Find Names</button>
    </div>
    <div class="cards-container">
      <CardsName
        @remove="removeName(index)"
        v-for="(name, index) in foundNames"
        :key="name"
        :index="index"
        :name="name"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: white;
  max-width: fit-content;
  background: steelblue;
  margin: 0 auto;
  text-align: center;
  padding: 3rem;
  padding-top: 1rem;
}

h1 {
  font-size: 3rem;
}

.options-container {
  max-width: fit-content;
  margin: 0 auto;
  padding: 1rem 2rem;
  background: #234;
  border-radius: 2rem;
}

.primary {
  background: salmon;
  color: white;
  font-weight: bold;
  cursor: pointer;
  outline: .2rem solid salmon;
  padding: .7rem;
  border-radius: 3rem;
  margin: 1rem;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 3rem;
}
</style>
