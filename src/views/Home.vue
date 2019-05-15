<template>
  <div>
    <ion-card v-for="(item, index) in wholeResponse" :key="index" style="border: 1px solid blue;">
      <ion-card-content>
        <img :src="item.Poster">
        <ion-card-header>
          <ion-card-title>{{item.Title}}</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <div>Ano: {{item.Year}}</div>
          <div>Tipo: {{item.Type}}</div>
        </ion-card-content>
        <ion-button color="dark" expand="full" @click="singleMovie(item.imdbID)">Ler Mais</ion-button>
      </ion-card-content>
    </ion-card>
    <!-- <ion-list>
      <ion-item v-for="(item, index) in wholeResponse" :key="index" @click="singleMovie(item.imdbID)">
        <img :src="item.Poster" class="thumb">
        <ion-label>{{item.Title}}</ion-label>
      </ion-item>
    </ion-list>-->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      wholeResponse: [],
      loading: true
    };
  },
  mounted() {
    axios
      .get(
        "http://www.omdbapi.com/?s=game&apikey=b76b385c&page=1&type=movie&Content-Type=application/json"
      )
      .then(response => {
        this.wholeResponse = response.data.Search;
        this.loading = false;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    singleMovie(id) {
      this.$router.push("/detail/" + id);
    }
  }
};
</script>

<style>
.thumb {
  width: 60px;
  height: 60px;
  border-radius: 30px;
  margin-right: 15px;
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>