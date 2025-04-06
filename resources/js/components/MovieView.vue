<template>
    <div>
      <h1>Movies</h1>
      <div v-for="movie in movies" :key="movie.id">
        <h2>{{ movie.title }}</h2>
        <p>{{ movie.description }}</p>
        <img :src="movie.poster" alt="Movie Poster" />
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from "vue";
  
  const movies = ref([]);
  
  const fetchMovies = async () => {
    try {
      const response = await fetch("/api/v1/movies");
      const data = await response.json();
      movies.value = data.movies;
    } catch (error) {
      console.error(error);
    }
  };
  
  onMounted(() => {
    fetchMovies();
  });
  </script>