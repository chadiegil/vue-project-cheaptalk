<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const postId = ref("");
const post = ref(null);

const router = useRoute();

postId.value = router.params.id;

const getPost = async (postId) => {};

onMounted(() => {
  getPost(postId.value);
});
</script>

<template>
  <h1>{{ postId }}</h1>
</template>
