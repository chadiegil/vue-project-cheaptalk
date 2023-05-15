<script setup>
import { ref } from "vue";
import { getFirestore } from "firebase/firestore";
import { useRoute, useRouter } from "vue-router";
import { app } from "../firebase/init.js";
import { doc, deleteDoc } from "firebase/firestore";
const postId = ref("");

const router = useRoute();
const routes = useRouter();

const db = getFirestore(app);

postId.value = router.params.id;

const deletePost = async (postId) => {
  await deleteDoc(doc(db, "posts", postId));
  routes.push("/");
};

const deleteHandler = () => {
  deletePost(postId.value);
};
</script>

<template>
  <h1>{{ postId }}</h1>

  <button @click.prevent="deleteHandler">Delete Post</button>
</template>
