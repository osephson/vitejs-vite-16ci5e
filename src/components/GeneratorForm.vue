<script setup>
import { ref, watch } from 'vue';
const emit = defineEmits(['generate']);

const count = ref(0);
const cols = ref(0);

const isDisabled = ref(true);
const errors = ref([]);

function validate() {
  const errs = [];
  if (count.value > 5) errs.push('Maximum count of cards is 5.');
  if (cols.value > 5) errs.push('Maximum number of rows/columns is 5.');

  errors.value = errs;
  return !errs.length;
}

function generate() {
  if (!validate()) return;

  emit('generate', count.value, cols.value);
}

watch([count, cols], ([newcount, newCols]) => {
  isDisabled.value = !(newcount && newCols);
});
</script>

<template>
  <div class="flex justify-center">
    <form
      class="
        text-xs
        bg-white
        p-1.5
        px-3
        rounded
        drop-shadow-[0_4px_4px_rgba(0,0,0,0.25)]
        w-343px
        sm:w-612px
      "
      @submit.prevent="generate"
    >
      <div class="sm:flex sm:justify-between">
        <div class="sm:flex">
          <div class="font-[Open_sans] py-1.5 pr-1">
            Generate
            <input
              type="number"
              v-model="count"
              :min="0"
              :class="errors.length && count > 5 && 'border-red'"
            />
            random cards,
          </div>
          <div class="font-[Open_sans] py-1.5">
            each with
            <input
              type="number"
              v-model="cols"
              :min="0"
              :class="errors.length && cols > 5 && 'border-red'"
            />
            rows/columns.
          </div>
        </div>

        <button
          class="
            px-13px
            py-7px
            bg-#0D6EFD
            rounded
            my-1.5
            w-full
            sm:w-auto
            disabled:opacity-[0.5]
          "
          :disabled="isDisabled"
        >
          <span class="text-white text-base font-bold"> Generate </span>
        </button>
      </div>

      <ul class="text-red">
        <li v-for="e in errors">{{ e }}</li>
      </ul>
    </form>
  </div>
</template>
