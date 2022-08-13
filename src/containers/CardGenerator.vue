<script setup>
import { ref } from 'vue';
import LetterCard from '../components/LetterCard.vue';

function generate() {
  console.log('hello');
}

const cardCount = ref(3);
const cols = ref(3);
</script>

<template>
  <div class="px-4 pt-[52px]">
    <h1 class="font-bold leading-[63px] text-5xl">Card Generator</h1>

    <form
      class="
        text-xs
        bg-[white]
        p-1.5
        px-3
        rounded
        drop-shadow-[0_4px_4px_rgba(0,0,0,0.25)]
        xsm:flex xsm:justify-between
      "
      @submit.prevent="generate"
    >
      <div class="xsm:flex">
        <div class="font-[Open_sans] my-1.5">
          Generate <input v-model="cardCount" /> random cards,
        </div>
        <div class="font-[Open_sans] my-1.5">
          each with <input v-model="cols" /> rows/columns.
        </div>
      </div>

      <button
        class="
          px-[13px]
          py-[7px]
          bg-[#0D6EFD]
          rounded
          text-[white]
          font-bold
          my-1.5
          w-full
          xsm:w-auto
        "
      >
        Generate
      </button>
    </form>

    <div
      v-for="index in cardCount"
      :key="index"
      class="flex justify-center my-[34px]"
    >
      <letter-card :cols="cols" />
    </div>
  </div>
</template>
