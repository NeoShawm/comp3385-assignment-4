<template>
  <form @submit.prevent="saveMovie">
    <div class="form-group mb-3">
      <label for="title" class="form-label">Movie Title</label>
      <input type="text" id="title" v-model="movie.title" name="title" class="form-control" />
    </div>
    <div class="form-group mb-3">
      <label for="description" class="form-label">Movie Description</label>
      <textarea id="description" v-model="movie.description" name="description" class="form-control"></textarea>
    </div>
    <div class="form-group mb-3">
      <label for="poster" class="form-label">Movie Poster</label>
      <input type="file" id="poster" @change="handlePosterChange" name="poster" class="form-control" />
    </div>
    <button type="submit" class="btn btn-primary">Save</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const movie = ref({
  title: '',
  description: '',
  poster: null,
});

const handlePosterChange = (event) => {
  movie.value.poster = event.target.files[0];
};

const saveMovie = () => {
  let formData = new FormData();
  formData.append('title', movie.value.title);
  formData.append('description', movie.value.description);
  formData.append('poster', movie.value.poster);

  fetch("/api/v1/movies", {
    method: 'POST',
    body: formData,
    headers: {
      'Accept': 'application/json'
    }
  })
  .then(response => response.json())
  .then(data => {
    console.log(data);
    // Handle success message or redirect
  })
  .catch(error => {
    console.error(error);
    // Handle error
  });
};
</script>