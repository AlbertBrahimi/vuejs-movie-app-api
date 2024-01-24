<template>
  <!-- Form for movie search -->
  <form @submit.prevent="searchMovies">
    <!-- Text input for search query -->
    <input type="text" placeholder="What are you searching for?" class="text" v-model="search">
    <!-- Submit button for the form -->
    <input type="submit" class="submit">
  </form>

  <!-- Container for dark mode switch -->
  <div class="switch-contanier">
    <label class="switch">
      <input type="checkbox"  @change="toggleDarkMode">
          <span class="slider">
              <svg class="slider-icon" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" role="presentation"><path fill="none" d="m4 16.5 8 8 16-16"></path></svg> 
          </span>
    </label>
</div>

  <!-- List of movies -->
  <div class="movieList">
    <!-- Loop through each movie in the movies array -->
    <div v-for="movie in movies" :key="movie.imdbID" class="movie">
      <!-- Link to movie details page with movie ID as a parameter -->
      <router-link :to="{ name: 'movieDetails', params: { id: movie.imdbID } }">
        <!-- Card for each movie -->
        <div class="card" style="width: 18rem;">
          <!-- Movie poster -->
          <img :src="movie.Poster" class="card-img-top" :alt="movie.Title">
          <div class="card-body">
            <!-- Movie title -->
            <h5 class="card-title"> <strong>{{ movie.Title }}</strong></h5>
            <!-- Movie year -->
            <p class="card-text">{{ movie.Year }}</p>
          </div>
        </div>
      </router-link>
    </div>
  </div>
</template>
<script>
import { ref,} from 'vue';
import env from '@/env';

export default {
  setup() {
    const search = ref('');
    const movies = ref([]);
    const darkMode = ref(true);

    const searchMovies = () => {
      fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = '';
        });
    };
    const toggleDarkMode = () => {
      document.body.classList.toggle('dark');
      darkMode.value = !darkMode.value;
    };

    return {
      search,
      movies,
      searchMovies,
      toggleDarkMode,
    };
  }
}
</script>

<style>
*{
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
form{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
}
.switch-contanier{
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 1rem;
}
/* The switch - the box around the slider */
.switch {
  font-size: 17px;
  position: relative;
  display: inline-block;
  margin: 0 auto;
  width: 3.5em;
  height: 2em;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #B0B0B0;
  border: 1px solid #B0B0B0;
  transition: .4s;
  border-radius: 32px;
  outline: none;
}

.slider:before {
  position: absolute;
  content: "";
  height: 2rem;
  width: 2rem;
  border-radius: 50%;
  outline: 2px solid #B0B0B0;
  left: -1px;
  bottom: -1px;
  background-color: #fff;
  transition: transform .25s ease-in-out 0s;
}

.slider-icon {
  opacity: 0;
  height: 12px;
  width: 12px;
  stroke-width: 8;
  position: absolute;
  z-index: 999;
  stroke: #222222;
  right: 60%;
  top: 30%;
  transition: right ease-in-out .3s, opacity ease-in-out .15s;
}

input:checked + .slider {
  background-color: #222222;
}

input:checked + .slider .slider-icon {
  opacity: 1;
  right: 20%;
}

input:checked + .slider:before {
  transform: translateX(1.5em);
  outline-color: #181818;
}
.text{
  width: 300px;
  padding: 20px;
  border-radius: 20px;
  border: 1px solid #0bac53;
  margin: 0 0.5rem;
}
.submit{
  border: none;
  border-radius: 10px; 
  padding: 20px;
  cursor: pointer;  
}
.submit:hover{
  background-color: #10753d;
  color: #fff;
}
.movieList{

  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  font-size: 30px;
  margin-top: 1rem;
  color: #0c0c0c;
  padding: 1rem;
  text-align: center;
  border-top: 10px solid black;
}
.movie {
  margin: 0 0.5rem;
  box-sizing: border-box; 
}
.card {
    height: 400px;
    margin-bottom: 20px;
    background-color: #23b95d;
    border: 2px solid black;
}
img{
  border-radius: 10px;
  cursor: pointer;
  height: 300px;
}
@media screen and (max-width: 400px) and  (min-width: 768px) {
  .movie {
    width: 100%; 
  }
}
</style>
