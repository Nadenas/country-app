<template>
<v-container fill-height fluid>
  <v-row
      justify="center">
      <v-col cols="8">
        <v-img
          max-height="400"
          max-width="800"
          v-bind:src= "image"
        ></v-img>
      </v-col>
      <v-col cols="4">
        <h1>{{ countryInfo.title }}</h1>
        <p><v-icon>mdi-account-group</v-icon> {{ countryInfo.population }}</p>
        <p><v-icon>mdi-web</v-icon> {{ countryInfo.continent }}</p>
        <div class="return-link">
          <NuxtLink to="/">Go back to countries</NuxtLink>
        </div>
      </v-col>
  </v-row>
</v-container>
</template>

<script>
import router from 'vue-router';
import countryData from "~/data.json";

export default {
  name: 'countryPage',
  asyncData ({ params }) {
      const countryInfo = countryData[params.id - 1]
      const image = countryInfo.src
      return { countryInfo, image }
  }
}
</script>

<style>
  h1 {
    color: coral;
    font-size: 3em;
    text-align: center;
  }

  p{
    font-size: 1.5em;
    text-align: center;
  }
  .return-link{
    text-align: center;
    margin-top: 40px;
    font-size: 1.2em;
  }
</style>