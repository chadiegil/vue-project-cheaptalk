<script setup>
import { onMounted, ref } from "vue";
import { getAuth, onAuthStateChanged, signOut } from "firebase/auth";
import { useRouter } from "vue-router";

const isLoggedIn = ref(false);

const router = useRouter();

let auth;
onMounted(() => {
  auth = getAuth();
  onAuthStateChanged(auth, (user) => {
    if (user) {
      isLoggedIn.value = true;
    } else {
      isLoggedIn.value = false;
    }
  });
});

const handleSignout = () => {
  signOut(auth).then(() => {
    router.push("/");
  });
};
</script>

<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/Feed">Feed</router-link>
    <router-link to="/register">Register</router-link>
    <router-link to="/sign-in">Login</router-link>
    <button @click="handleSignout" v-if="isLoggedIn">Sign out</button>
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
