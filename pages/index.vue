<template>
  <div>
    <!--<myFavCountries/>-->
    <SearchBar @search="handleSearch"/> 

    <CountryCards :cards="filteredCards"/>
    
  </div>
  
</template>

<script>
import SearchBar from '~/components/searchBar'
import CountryCards from '~/components/countryCards'



export default {
  components: {
    SearchBar,
    CountryCards,
  },
  data() {
    return {
      cards: CountryCards.data().cards,
      filteredCards: CountryCards.data().cards
    }
  },
  methods: {
    
    handleSearch(value){
      if(value && value.length > 0) {
        this.filteredCards = this.cards.filter(i => {
          const val = value.toLowerCase();
          const card = i.title.toLowerCase();
          return card.includes(val)
        })
      } else {
        this.filteredCards = this.cards;
      }
    }
  }
}
</script>

<style>

</style>