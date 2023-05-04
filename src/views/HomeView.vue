<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://m.media-amazon.com/images/I/71TZ8BmoZqL._AC_SL1000_.jpg"
          alt="LOTR Poster"
          class="featured-img"
        />
        <div class="detail">
          <h3>The Fellowship of the Ring</h3>
          <p>
            The future of civilization rests in the fate of the One Ring, which
            has been lost for centuries. Powerful forces are unrelenting in
            their search for it. But fate has placed it in the hands of a young
            Hobbit named Frodo Baggins (Elijah Wood), who inherits the Ring and
            steps into legend. A daunting task lies ahead for Frodo when he
            becomes the Ringbearer - to destroy the One Ring in the fires of
            Mount Doom where it was forged.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="movie-type">{{ movie.Type }}</div>
          </div>
          <div class="movie-detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value !== "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style>
.feature-card {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.feature-img {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;
  position: relative;
  z-index: 0;
}

.detail {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 16px;
  z-index: 1;
}

h3 {
  color: #fff;
  margin-bottom: 16px;
}
p {
  color: #fff;
}
.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
}

input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}

input[type="text"] {
  width: 100%;
  color: #fff;
  background-color: #496583;
  font-size: 20px;
  padding: 10px 16px;
  border-radius: 8px;
  margin-bottom: 15px;
  transition: 0.4s;
}

input[type="text"]::placeholder {
  color: #f3f3f3;
}
input[type="text"]:focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}
input[type="submit"] {
  width: 100%;
  max-width: 300px;
  background-color: #42b883;
  padding: 16px;
  border-radius: 8px;
  color: #fff;
  font-size: 20px;
  text-transform: uppercase;
  transition: 0.4s;
}
input[type="submit"]:active {
  background-color: #3b8070;
}
/* .movies-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  max-width: 1200px;
}

.movie {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  max-width: 300px;
  margin: 16px;
  padding: 16px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
} */

.movies-list {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin: 0px 10px;
}

.movie {
  width: 200px;
  height: 100%;
  /* width: 100%;
  max-width: 50%;
  flex: 1 1 50%; */
  margin: 8px 8px;
  box-shadow: 3px 6px 3px 6px rgba(0, 0, 0, 0.2);

  /* padding: 16px 8px; */
}

.movie-link {
  display: flex;
  flex-direction: column;
  height: 375px;
}
.product-image {
  position: relative;
  display: block;
}

.product-image img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}
.movie-type {
  position: absolute;
  padding: 8px 16px;
  background-color: #42b883;
  color: #fff;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}
.movie-detail {
  background-color: #496583;
  padding: 16px 8px;
  height: 100px;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}
.year {
  color: #aaa;
  font-size: 14px;
}
.movie h3 {
  color: #fff;
  font-weight: 600;
  font-size: 18px;
}
</style>
