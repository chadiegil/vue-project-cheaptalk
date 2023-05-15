<script setup>
import { ref, onMounted, computed } from "vue";
import { db } from "../firebase/init.js";

import { collection, getDocs } from "firebase/firestore";

import Spinner from "../components/Spinner.vue";

const authors = ref([]);
const isLoading = ref(true);

onMounted(async () => {
  const querySnapshot = await getDocs(collection(db, "users"));

  const authorLocal = [];

  querySnapshot.forEach((doc) => {
    const auth = {
      id: doc.id,
      name: doc.data().name,
      password: doc.data().password,
      gender: doc.data().gender,
    };

    authorLocal.push(auth);
  });
  authors.value = authorLocal;
  isLoading.value = false;
});

const genderClass = computed(() => {
  return (gender) => {
    gender === "male" ? "blue" : "pink";
  };
});
</script>
<template>
  <div v-if="isLoading">
    <Spinner />
  </div>
  <div v-else>
    <h1>Authors</h1>
    <div class="flex">
      <div v-for="author in authors" :key="author.id">
        <div class="card item">
          <div class="card-details">
            <p class="text-title">{{ author.name }}</p>
            <p class="text-body">Here are the details of the card</p>
          </div>
          <button class="card-button" :class="genderClass(author.gender)">
            {{ author.gender }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 190px;
  height: 254px;
  border-radius: 20px;
  background: #f5f5f5;
  position: relative;
  padding: 1.8rem;
  border: 2px solid #c3c6ce;
  transition: 0.5s ease-out;
  overflow: visible;
}

.card-details {
  color: black;
  height: 100%;
  gap: 0.5em;
  display: grid;
  place-content: center;
}

.card-button {
  transform: translate(-50%, 125%);
  width: 60%;
  border-radius: 1rem;
  border: none;
  background-color: #008bf8;
  color: #fff;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  position: absolute;
  left: 50%;
  bottom: 0;
  opacity: 0;
  transition: 0.3s ease-out;
}

.text-body {
  color: rgb(134, 134, 134);
}

/*Text*/
.text-title {
  font-size: 1em;
  font-weight: bold;
}

/*Hover*/
.card:hover {
  border-color: #008bf8;
  box-shadow: 0 4px 18px 0 rgba(0, 0, 0, 0.25);
}

.card:hover .card-button {
  transform: translate(-50%, 50%);
  opacity: 1;
}

/* card */

.flex {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 100px;
}
.item {
  flex: 1;
  max-width: 300px;
}
.blue {
  color: blue;
}
.pink {
  color: rgb(223, 94, 115);
}
</style>
