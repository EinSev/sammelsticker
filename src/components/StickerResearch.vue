<script setup>
import {ref} from "vue";

/**
 *
 * @type {Ref<UnwrapRef<number>>}
 */
const inputNumber = ref(null);
let error = ref(false);
let result = ref(null);
let duplicate = ref(null);


const missingNumbers = [
  3, 7, 10, 12, 14, 16, 20, 21, 23, 24, 25, 30, 32, 39, 51, 52, 56, 57, 58, 63, 64, 74, 83, 94, 103, 104, 106, 114, 116, 120, 133, 134, 136, 137, 141, 142, 144, 145, 148, 151, 156, 157, 158, 159, 170, 176, 180,
];

const duplicateList = [
  [1, 1],
  [4, 3],
  [5, 3],
  [11, 4],
  [17, 1],
  [22, 1],
  [26, 1],
  [28, 1],
  [29, 2],
  [31, 2],
  [33, 1],
  [34, 1],
  [35, 2],
  [37, 2],
  [38, 4],
  [40, 2],
  [41, 1],
  [43, 5],
  [44, 2],
  [46, 3],
  [47, 1],
  [48, 2],
  [50, 1],
  [59, 2],
  [60, 4],
  [62, 1],
  [66, 3],
  [68, 1],
  [70, 1],
  [71, 1],
  [72, 1],
  [73, 1],
  [75, 1],
  [80, 2],
  [82, 1],
  [85, 1],
  [95, 1],
  [96, 1],
  [98, 1],
  [100, 1],
  [108, 3],
  [110, 3],
  [119, 2],
  [122, 1],
  [123, 5],
  [125, 2],
  [126, 1],
  [128, 2],
  [130, 1],
  [132, 1],
  [143, 2],
  [150, 1],
  [153, 1],
  [155, 1],
  [160, 1],
  [161, 1],
  [163, 2],
  [164, 1],
  [165, 1],
  [167, 1],
  [168, 2],
  [173, 2],
  [174, 4],
  [176, 3],
  [179, 3]
]

const checkNumber = () => {
  let input = parseInt(inputNumber.value);
  error.value = false;
  duplicate.value = null;
  result.value = null;

  if (input <= 180) {

    result.value = missingNumbers.includes(input);

    duplicateList.forEach((row) => {
      if (row[0] === input) {
        duplicate.value = row[1];
      }
    });

  } else error.value = !isNaN(input);

  console.log(duplicate.value)
};

</script>

<template>
  <div class="flex flex-col justify-center items-center mt-36">
    <h1 class="text-3xl font-bold mb-4">Das große Disney-100 Sticker-Sammeln der 4BI</h1>

    <div class="flex flex-col justify-center items-center">
      <h2 class="text-xl font-bold mb-4">Haben wir diese Nummer schon?</h2>
      <div>
        <input v-model="inputNumber" @input="checkNumber" type="number" min="1" max="180" id="numberInput"
               placeholder="Nummer (1-180)" autofocus class="p-3 border border-gray-300 rounded w-40">
        <p v-if="error" class="font-bold">Nicht zwischen 0 und 180</p>
      </div>

      <div v-if="((result !== null) && (inputNumber !== null)) && error === false" class="mt-4 text-center text-xl">
        <p v-if="!result" class="text-red-600">Die Nummer <strong>{{ inputNumber }}</strong> ist bereits in unserer
          Sammlung</p>
        <p v-if="duplicate !== null">Wir haben diesen Sticker sogar <strong>{{ duplicate }}x</strong> doppelt</p>
        <p v-if="result" class="text-green-600 font-semibold">Die Nummer <strong>{{ inputNumber }}</strong> könnten wir
          noch
          gebrauchen</p>
      </div>
    </div>
    <div class="fixed bottom-0 mb-10">
      <button class="bg-green-600 text-white font-bold py-2 px-4 rounded mr-10"><a href="https://htl3r-my.sharepoint.com/:x:/g/personal/0212_htl_rennweg_at/EdPVnY_LQFxPqIQR447hCMABuMT-_lISGcTAzzenfwQh3Q?e=cey22i" target="_blank">Fehlende als Excel</a></button>
      <button class="bg-green-600 text-white font-bold py-2 px-4 rounded"><a href="https://htl3r-my.sharepoint.com/:x:/g/personal/0212_htl_rennweg_at/ETuNs2z6NPpNo0i1rVKVx-gBaxKez5BN7RbwuM3xmbOQ3g?e=3vrEEI" target="_blank">Doppelte als Excel</a></button>
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
