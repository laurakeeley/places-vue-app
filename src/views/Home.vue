<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>Name: <input type="text" v-model="newPlaceParams.name" /></div>
    <div>Address: <input type="text" v-model="newPlaceParams.address" /></div>
    <p>newPlaceParams: {{ newPlaceParams }}</p>
    <button v-on:click="createPlaces">New Place</button>
    <div v-for="place in places" v-bind:key="place.id">
      <p>Name: {{ place.name }}</p>
      <p>Address: {{ place.address }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Places",
      places: [],
      newPlaceParams: {},
    };
  },
  created: function () {
    this.indexPlaces();
  },
  methods: {
    indexPlaces: function () {
      axios.get("http://localhost:3000/places").then((response) => {
        console.log(response.data);
        this.places = response.data;
      });
    },
    createPlaces: function () {
      axios
        .post("http://localhost:3000/places", this.newPlaceParams)
        .then((response) => {
          console.log(response.data);
          this.places.push(response.data);
        });
    },
  },
};
</script>
