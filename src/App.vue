<template>
  <div class="movies-list">
    <div class="movie"
         v-for="(movie, movieIndex) in movies"
         :key="movie.id">

      <div class="absolute">
        <StarIcon :class="movie.rating !== null ? 'text-yellow-500' : 'text-gray-500'"
                  class="w-16"/>
        <h2 class="absolute top-5 left-7 ">{{ movie.rating ? movie.rating : '-' }}</h2>
      </div>
      <img :src="movie.image" :alt="movie.name">
      <div class="movie-description">
        <h1>{{movie.name}}</h1>

        <div class="genres">
          <span v-for="(genre, index) in movie.genres" class="genre" :key="index">{{ genre }}</span>
        </div>

        <p>{{movie.description}}</p>
        <div class="rating">
          <p>Rating: ({{ movie.rating }}/5) </p>

            <button
                v-for="rate in 5"
                class="star-button"
                :class="rate <= movie.rating ? 'text-yellow-500' : 'text-gray-500'"
                :disabled="rate === movie.rating"
                @click.once="updateRating(rate, movieIndex)"
            >
              <StarIcon />
            </button>

        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { items } from "./movies.json";
import { StarIcon } from "@heroicons/vue/24/solid";
import {ref} from 'vue'

const movies = ref(items)

function updateRating(rating, movieIndex) {
  movies.value[movieIndex].rating = rating
}

</script>


<style scoped>

.movies-list {
  display: grid; 
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin: 5rem 0;
}

.movie {
  border-radius: 15px;
  overflow: auto;
  background-color: #FFF;
  width: 400px;
}

.movie img {
  object-fit: cover;
  width: 100%;
  height: 500px;
}

.movie-description {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h1 {
  font-size: 1.5rem;
  font-weight: bold;
}

.genres {
  display: flex;
  flex-direction: row;
}

.genre {
  color: #fff;
  background-color: #6466F1;
  border-radius: 10rem;
  width: fit-content;
  padding: .2rem .5rem;
  margin: 0 .2rem;
}

.rating {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 2rem;
}

.star-button {
  width: 32px;
  height: 32px;
}
</style>