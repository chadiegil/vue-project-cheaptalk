<script setup></script>
<template>
  <div v-for="post in posts" :key="post.id">
    {{ post.title }}
  </div>
</template>

<style scoped></style>
