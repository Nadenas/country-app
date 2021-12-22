<template>
  <v-row dense>
    <div class="mx-auto my-6">
      
    <v-menu offset-y >
      <template v-slot:activator="{ on, attrs }">
        <v-btn 
          class="fav-countries"
          color="pink"
          dark
          v-bind="attrs"
          v-on="on"
        >
         <v-icon>mdi-cards-heart</v-icon>
         <span>My countries</span>
        </v-btn>
      </template>
      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
        >
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
    <v-col cols="12">
      <v-card-actions class="justify-center">
        <v-btn
          depressed
          @click="sortBy('title')">
          Order alphabetically
        </v-btn>
        <v-btn
          depressed
          dark
          @click="sortByDesc('population')">
          Order by more population
        </v-btn>
        <v-btn
          depressed
          dark
          @click="sortBy('population')">
          Order by less population
        </v-btn>
      </v-card-actions>
    </v-col>
    <v-col
      v-for="card in cards"
      :key="card.title"
      :cols="card.flex"
    >
      <v-card>       
        <v-img
          :src="card.src"
          class="white--text align-end"
          gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
          height="200px"
        >
           <NuxtLink class="view-more" :to="`/countries/${card.id}`">
            <v-btn icon>
              <v-icon>mdi-eye</v-icon>
            </v-btn>
          </NuxtLink>
          <v-card-title v-text="card.title"></v-card-title>
        </v-img>

        <v-card-actions>
          <v-icon>mdi-account-group</v-icon>
          <span class="population-info">{{card.population}}</span>
          <v-spacer></v-spacer>
          <v-btn
            class="mx-2"
            fab
            dark
            small
            color="pink"
            @click="addToFavorites(items, card.id)"
          >
            <v-icon dark>
              mdi-cards-heart
            </v-icon>
          </v-btn>
          <v-btn
            class="mx-2"
            fab
            dark
            small
            color="green"
            @click="editPopulation(card.id)"
          >
            <v-icon dark>
              mdi-file-document-edit-outline
            </v-icon>
          </v-btn>
          <v-btn
            class="mx-2"
            fab
            dark
            small
            color="red"
            @click="deleteCountryCard()"
          >
            <v-icon dark>
              mdi-delete
            </v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import router from 'vue-router';
import countryData from "~/data.json";
import { countries } from '~/countryArray.js';

export default {
  name: 'countryPage',
  props:{
    cards:{
      type: Array
    }
  },
  data: function () {
    return {
    cards: countries,
    search:'',
    items: [],
    added: true
    //population: 
    }
  },
  methods: {
    sortBy(prop) {
      this.cards.sort((a,b) => a[prop] < b[prop] ? -1 : 1)
    },
    sortByDesc(prop) {
      this.cards.sort((a,b) => b[prop] < a[prop] ? -1 : 1)
    },
    deleteCountryCard(index){
      this.cards.splice(index,1)
    },
    editPopulation(id){
      this.$refs["population"].isDisabled = false
      //this.cards[id].population
    },
    addToFavorites(items,id){
      if(!items.includes(this.cards[id-1].title)){
        items.push({title: this.cards[id-1].title})
      }
    }
  }    
}
</script>

<style>
 .population-info{
   color: coral;
   margin-left: 8px;
 }
 .fav-countries{
   color: white;
 }
 .view-more{
   float: right;
   margin-bottom: 130px;
   text-decoration: none;
   font-size: 2em;
 }
</style>