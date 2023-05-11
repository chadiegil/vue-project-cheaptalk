<script setup>
import { ref, onMounted } from "vue";

const count = ref(0);
const isTrue = ref(false);

const increment = () => {
  count.value++;
};

const showBtn = () => {
  isTrue = !isTrue;
};

// onMounted(() => {
//   console.log(`The initial value is ${count.value}`);
// });
</script>

<template>
  <button @click="isTrue = !isTrue">Show button</button>
  <button @click="increment" v-if="isTrue">Count is {{ count }}</button>
</template>
