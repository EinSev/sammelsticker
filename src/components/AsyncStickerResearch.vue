<script setup>
import {supabase} from "../clients/supabase.js";
import {ref} from "vue";

/**
 *
 * @type {Ref<UnwrapRef<number>>}
 */
const inputNumber = ref(null);

let error = ref(false);
let result = ref(null);
let duplicateAmount = ref(null);


const {data: missingList } = await supabase
    .from('missing')
    .select('*');


const {data: duplicateList } = await supabase
    .from('duplicate')
    .select('*');


const checkNumber = () => {
  let input = parseInt(inputNumber.value);
  error.value = false;
  duplicateAmount.value = null;
  result.value = null;

  if (input <= 180) {

    result.value = missingList.includes(input);

    duplicateList.forEach((row) => {
      if (row["id"] === input) {
        duplicateAmount.value = row["amount"];
      }
    })

  } else error.value = !isNaN(input);

};
</script>

<template>
  <div class="flex flex-col justify-center items-center">
    <h2 class="text-xl font-bold mb-4">Haben wir diese Nummer schon?</h2>
    <div>
      <input v-model="inputNumber" @input="checkNumber" type="number" min="1" max="180" id="numberInput"
             placeholder="# (1-180)" autofocus class="p-3 border border-gray-300 rounded w-48">
      <p v-if="error" class="font-bold text-red-600 text-center">Nicht zwischen 0 und 180</p>
    </div>

    <div v-if="((result !== null) && (inputNumber !== null)) && error === false" class="mt-4 text-center text-xl">
      <p v-if="!result" class="text-red-600">Die Nummer <strong>{{ inputNumber }}</strong> ist bereits in unserer
        Sammlung</p>
      <p v-if="duplicateAmount !== null">Wir haben diesen Sticker sogar <strong>{{ duplicateAmount }}x</strong> doppelt</p>
      <p v-if="result" class="text-green-600 font-semibold">Die Nummer <strong>{{ inputNumber }}</strong> könnten wir
        noch
        gebrauchen</p>
    </div>
  </div>
</template>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>