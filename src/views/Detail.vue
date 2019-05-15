<template>
  <div>
    <ion-card>
      <ion-card-header>
        <ion-label>{{singleMovie.Title}}-{{singleMovie.Year}}</ion-label>
      </ion-card-header>
      <ion-card-content>
        <ion-img :src="singleMovie.Poster"></ion-img>
        <p>{{ singleMovie.Plot}}</p>
        <h3>Actors:</h3>
        {{singleMovie.Actors}}
        <h4>Awards:</h4>
        {{singleMovie.Awards}}
        <p>Genre: {{singleMovie.Genre}}</p>
        <ion-button color="tertiary" extend="full" @click="$router.go(-1)">Voltar</ion-button>
      </ion-card-content>
    </ion-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      singleMovie: "",
      dialog: false,
      loading: true,
      ratings: ""
    };
  },
  mounted() {
    axios
      .get(
        "http://www.omdbapi.com/?apikey=b76b385c&i=" +
          this.id +
          "&Content-Type=application/json"
      )
      .then(response => {
        this.singleMovie = response.data;
        this.ratings = this.singleMovie.Ratings;
        this.ratings.forEach(function(element) {
          element.Value = parseFloat(element.Value.split(/\/|%/)[0]);
          element.Value =
            element.Value <= 10 ? element.Value / 2 : element.Value / 20;
        });
        this.loading = false;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    back() {
      this.$router.push("/");
    }
  }
};
</script>
