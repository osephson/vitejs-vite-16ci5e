<script setup>
import { ref, watch, readonly } from 'vue';
import LetterCard from '../components/LetterCard.vue';
import GeneratorForm from '../components/GeneratorForm.vue';

const count = ref(0);
const cols = ref(0);
const generatedCount = ref(0);

function generate(cardCount, cardCols) {
  generatedCount.value += cardCount;

  count.value = cardCount;
  cols.value = cardCols;
}
</script>

<template>
  <div class="flex justify-center">
    <div class="pt-52px">
      <h1 class="font-bold leading-63px text-5xl text-center sm:text-left">
        Card Generator
      </h1>

      <generator-form @generate="generate" />

      <div
        v-if="count && cols"
        v-for="index in count"
        :key="generatedCount + index"
        class="flex justify-center my-36px sm:my-34px"
      >
        <letter-card :cols="cols" />
      </div>
    </div>
  </div>
</template>
