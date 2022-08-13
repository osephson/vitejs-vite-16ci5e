<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  cols: Number,
});

const letters = ref([]);

const generateLetters = (cnt) => {
  const letters = [];
  const result = [];
  for (let i = 0; i < 26; i++) letters.push(i);
  while (result.length < cnt) {
    const index = Math.floor(Math.random() * letters.length);
    result.push(letters[index]);
    letters.splice(index, 1);
  }

  return result;
};

onMounted(() => {
  letters.value = generateLetters(props.cols);
});
</script>

<template>
  <!-- <span>{{ randomLetters[0] }}</span> -->
  <div>
    <span v-for="letter in letters">{{ letter + ' ' }}</span>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
