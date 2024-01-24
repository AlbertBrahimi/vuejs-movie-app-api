<template>
    <div class="movie-details">
    <h1>{{ movie.Title }}</h1>
    <img :src="movie.Poster" alt="{{ movie.Title }}" class="movie-poster">
    <p>{{ movie.Plot }}</p>
    <div>
        <strong>Director:</strong> {{ movie.Director }} <br>
        <strong>Rating</strong> {{ movie.imdbRating}}

    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount} from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env';
export default {
 setup(){
    const movie = ref([]);
    const route = useRoute();

    onBeforeMount(() => {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
            movie.value = data;
        });
    });
    return {
        movie
    };

 }
}
</script>

<style scoped>
.movie-details {
  text-align: center;
  padding: 2rem;
  font-size: large;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.movie-poster {
  width: 200px;
  height: 300px;
  margin: 1rem auto;
  display: block;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

h1 {
  font-size: 24px;
  color: #333;
}

p {
  font-size: 16px;
  color: #666;
}

</style>