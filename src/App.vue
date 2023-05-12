<script setup>
import { onMounted, ref } from "vue";
import { getAuth, onAuthStateChanged, signOut } from "firebase/auth";
import { useRouter } from "vue-router";
import Navbar from "./components/Navbar.vue";
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
  <Navbar />
  <router-view />
</template>

<style scoped>
/* nav {
  width: 600px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  text-decoration: none;
} */
</style>
