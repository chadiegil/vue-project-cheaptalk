<script setup>
import { ref } from "vue";

import db from "../firebase/init.js";
import { collection, addDoc } from "firebase/firestore";
import { onMounted } from "vue";

const title = ref("");
const description = ref("");

const createUser = async () => {
  const colref = collection(db, "posts");

  const dataObj = {
    title: title.value,
    description: description.value,
  };

  const docRef = await addDoc(colref, dataObj);
  console.log("Document was created with id: ", docRef.id);
};

console.log(title);
console.log(description);
onMounted(() => {
  //   createUser();
});
</script>

<template>
  <h1>Create a post</h1>

  <form @submit.prevent="createUser">
    <input type="text" placeholder="Title" v-model="title" />
    <input type="text" placeholder="Description" v-model="description" />
    <button>Post</button>
  </form>
</template>

<style scoped></style>
