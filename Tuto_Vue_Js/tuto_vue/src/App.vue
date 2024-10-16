<template>
  <h1>Bonjour {{ firstName }}</h1>
  <p v-bind:id="count2">Comment ça va ?</p>

  <p>compteur 1 : {{ count }}</p>
  <p>compteur 2 : {{ count2 }} <div v-html="firstname"></div></p>  <!-- v-html="" pour injecter html -->
  <p v-bind:id="`p-${count2}`">Compteur 2</p>  <!--  2points indique que c'est dinamique    -->
  <p :id="`p-${count2}`">Compteur 2.1</p> <!-- avec les 2 points: prend la valeur -->
  <p id="`p-${count2}`">Compteur 2.2</p>  <!-- sans les 2 points: prend la chaine de caractère -->
  <p :style="{color: count2 > 5 ? 'red': 'green'}">Compteur 2.2</p> 

  <ul>
    <li v-for="movie in movies" :key="movie"> <!-- :key=""  pour lier l'element avec le li -->
      {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>

  <form action="" @submit.prevent="addMovie">
    <input type="text" placeholder="Nouveau film" v-model="movieName">
    <button>Ajouter Film</button>
  </form>
  <!-- ************************* -->

  <button v-on:click="increment">Incrementer</button>
  <button v-on:click="decrement">Decrementer</button>
  <!-- equivalent -->
  <button @click="increment">Incrementer</button>
  <button @click="count2++">Incrementer</button>
  <button @click="decrement">Decrementer</button>

  <button @click="sortMovies">Réorganiser</button>

  <div v-show="count2 >= 5">Bravo, vous avez cliqué plus de 5 fois</div>
  <div v-if="count2 >= 5">Bravo, vous avez cliqué plus de 5 fois</div>
  <div v-else>Vous avez cliqué moins de 5 fois</div>

  <!-- ************************* -->
</template>

<script setup>
import { ref } from 'vue'

const firstName = "John";
const count = ref(0)
const count2 = ref(0)
count.value = 3

setInterval(() => {
  count.value++
}, 1000);

const increment = () => {
  count2.value++
}
const decrement = () => {
  count2.value--
}
const decrement2 = (event) => {
  console.log(event)
  count2.value--
}
const firstname = '<span>Demo</span>'   /* injecter html */
const movies = ref([
  'Matrix',
  'Lilo & Stitch',
  'Titanic'
])
const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m !== movie)
}
const sortMovies = () => {
  movies.value.sort()
}
const movieName = ref('')
const addMovie = () => {
  movies.value.push(movieName.value)
  movieName.value = ''
}

</script>

<style>
  h1{
    color: red;
  }
</style>