<script setup></script>

<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/Feed">Feed</router-link>
    <router-link to="/register">Register</router-link>
    <router-link to="/sign-in">Login</router-link>
  </nav>

  <router-view />
</template>

<style scoped>
nav {
  /* background: red; */
  width: 600px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  text-decoration: none;
}
</style>
