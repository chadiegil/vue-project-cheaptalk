<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import { getFirestore, getDoc, doc, setDoc } from "firebase/firestore";
import { app } from "../firebase/init.js";

const postId = ref("");
const post = ref(null);

const router = useRoute();
const db = getFirestore(app);

const singlePost = ref([]);
postId.value = router.params.id;

const getPost = async (postId) => {
  const docRef = doc(db, "posts", postId);
  getDoc(docRef).then((doc) => {
    singlePost.value = doc.data();
  });
};

const updatePost = async (postId) => {
  const docRef = doc(db, "posts", postId);
  //   setDoc(docRef, singlePost.value)
  //     .then((docRef) => {
  //       console.log("Entire Document has been updated successfully");
  //     })
  //     .catch((error) => {
  //       console.log(error);
  //     });
};

onMounted(() => {
  getPost(postId.value);
  updatePost(postId.value, singlePost);
});
</script>

<template>
  <form class="form">
    <p class="form-title">Edit Post</p>

    <div class="input-container">
      <label for="title">Title</label>
      <input type="text" v-model="singlePost.title" />
      <span> </span>
    </div>
    <div class="input-container">
      <label for="title">Description</label>

      <input type="text" v-model="singlePost.description" />
    </div>
    <div class="input-container">
      <label for="title">Category</label>

      <input type="text" placeholder="Category" v-model="singlePost.category" />
    </div>
    <button type="submit" class="submit" @click.prevent="updatePost">
      Update
    </button>
  </form>
</template>
<style scoped>
.form {
  background-color: #fff;
  display: block;
  padding: 1rem;
  max-width: 350px;
  border-radius: 0.5rem;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.form-title {
  font-size: 1.25rem;
  line-height: 1.75rem;
  font-weight: 600;
  text-align: center;
  color: #000;
}

.input-container {
  position: relative;
}

.input-container input,
.form button {
  outline: none;
  border: 1px solid #e5e7eb;
  margin: 8px 0;
}

.input-container input {
  background-color: #fff;
  padding: 1rem;
  padding-right: 3rem;
  font-size: 0.875rem;
  line-height: 1.25rem;
  width: 300px;
  border-radius: 0.5rem;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

.submit {
  display: block;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  padding-left: 1.25rem;
  padding-right: 1.25rem;
  background-color: #4f46e5;
  color: #ffffff;
  font-size: 0.875rem;
  line-height: 1.25rem;
  font-weight: 500;
  width: 100%;
  border-radius: 0.5rem;
  text-transform: uppercase;
}

.signup-link {
  color: #6b7280;
  font-size: 0.875rem;
  line-height: 1.25rem;
  text-align: center;
}

.signup-link a {
  text-decoration: underline;
}
</style>
