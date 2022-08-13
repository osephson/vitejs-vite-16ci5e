<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  cols: Number,
});

const letters = ref([]);

const generateLetters = (cnt) => {
  const letters = [];
  const result = [];
  for (let i = 0; i < 26; i++) letters.push(String.fromCharCode(65 + i));
  while (result.length < cnt) {
    const index = Math.floor(Math.random() * letters.length);
    result.push(letters[index]);
    letters.splice(index, 1);
  }

  return result;
};

onMounted(() => {
  letters.value = generateLetters(props.cols * props.cols);
});
</script>

<template>
  <div class="bg-black p-1.5 rounded inline-block">
    <div v-for="i in cols" :key="i" class="flex">
      <div
        v-for="j in cols"
        :key="j"
        class="
          text-4xl
          bg-white
          m-1.5
          flex
          items-center
          justify-center
          w-60px
          h-60px
        "
      >
        <span class="font-black text-4xl leading-47px">{{
          letters[(i - 1) * cols + (j - 1)]
        }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
