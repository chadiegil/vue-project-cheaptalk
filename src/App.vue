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
    <div class="navbar">
      <div class="logo">Cheaptalk</div>
      <div class="menu">
        <ul>
          <li>
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/Feed">Feed</router-link>
          </li>
          <li>
            <router-link to="/register">Register</router-link>
          </li>
          <li>
            <router-link to="/sign-in">Login</router-link>
          </li>
          <li>
            <button @click="handleSignout" v-if="isLoggedIn">Sign out</button>
          </li>
        </ul>
      </div>
    </div>
  </nav>

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

@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
nav {
  /* position: fixed;
  left: 0;
  top: 0; */
  width: 100%;
  height: 75px;
  background: #2980b9;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
}
nav .navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  max-width: 90%;
  background: #2980b9;
  margin: auto;
}
nav .navbar .logo a {
  color: #fff;
  font-size: 27px;
  font-weight: 600;
  text-decoration: none;
}
nav .navbar .menu ul {
  display: flex;
}
.navbar .menu li {
  list-style: none;
  margin: 0 15px;
}
.navbar .menu li a {
  color: #fff;
  font-size: 17px;
  font-weight: 500;
  text-decoration: none;
}
section {
  display: flex;
  height: 100vh;
  width: 100%;
  align-items: center;
  justify-content: center;
  color: #96c7e8;
  font-size: 70px;
}
.logo {
  color: white;
  font-weight: bold;
  font-size: 20px;
}
.button a {
  position: fixed;
  bottom: 20px;
  right: 20px;
  color: #fff;
  background: #2980b9;
  padding: 7px 12px;
  font-size: 18px;
  border-radius: 6px;
  box-shadow: rgba(0, 0, 0, 0.15);
}
</style>
