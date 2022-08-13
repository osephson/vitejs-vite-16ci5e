<script setup>
import { ref, watch, readonly } from 'vue';
import LetterCard from '../components/LetterCard.vue';

const count = ref(0);
const cols = ref(0);

const isDisabled = ref(true);
const errors = ref([]);

const realCount = ref(0);
const realCols = ref(0);

const generatedCount = ref(0);

function validate() {
  const errs = [];
  if (count.value > 5) errs.push('Maximum count of cards is 5.');
  if (cols.value > 5) errs.push('Maximum number of rows/columns is 5.');

  errors.value = errs;
  return !errs.length;
}

function generate() {
  if (!validate()) return;
  realCount.value = count.value;
  realCols.value = cols.value;

  generatedCount.value += count.value;
}

watch([count, cols], ([newcount, newCols]) => {
  isDisabled.value = !(newcount && newCols);
});
</script>

<template>
  <div class="px-4 pt-52px xsm:px-76px">
    <h1 class="font-bold leading-63px text-5xl">Card Generator</h1>

    <form
      class="
        text-xs
        bg-white
        p-1.5
        px-3
        rounded
        drop-shadow-[0_4px_4px_rgba(0,0,0,0.25)]
      "
      @submit.prevent="generate"
    >
      <div class="xsm:flex xsm:justify-between">
        <div class="xsm:flex">
          <div class="font-[Open_sans] my-1.5 mr-1">
            Generate
            <input type="number" v-model="count" :min="0" /> random cards,
          </div>
          <div class="font-[Open_sans] my-1.5">
            each with
            <input type="number" v-model="cols" :min="0" /> rows/columns.
          </div>
        </div>

        <button
          class="
            px-13px
            py-7px
            bg-#0D6EFD
            rounded
            text-white
            font-bold
            my-1.5
            w-full
            xsm:w-auto
            disabled:opacity-[0.5]
          "
          :disabled="isDisabled"
        >
          Generate
        </button>
      </div>

      <ul class="text-red">
        <li v-for="e in errors">{{ e }}</li>
      </ul>
    </form>

    <div
      v-if="realCount && realCols"
      v-for="index in realCount"
      :key="generatedCount + index"
      class="flex justify-center my-34px"
    >
      <letter-card :cols="realCols" />
    </div>
  </div>
</template>
