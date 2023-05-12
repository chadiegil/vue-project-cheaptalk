<script setup>
// import { ref, onMounted } from "vue";
// import db from "../firebase/init.js";
// import { collection, doc, getDocs } from "firebase/firestore";

// const colRef = collection(db, "posts");
// const docsSnap = await getDocs(colRef);

// const posts = [];

// docsSnap.forEach((doc) => {
//   // console.log(doc.data());
//   console.log(doc.data());
//   posts.push(doc.data());
// });
</script>
<template>
  <h1>Home</h1>
  <div>
    <p v-for="post in posts" :key="post.id">
      {{ post.title }}
    </p>
  </div>
</template>

<style scoped></style>
