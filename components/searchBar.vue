<template>
  <v-container fill-height fluid>
    <v-row>
      <v-col>
        <v-text-field 
          type="text"
          v-model="search" 
          label="Search a country" 
          class="mx-auto mt-10 mb-4"
          prepend-icon="mdi-magnify"
          @change="onChange"
          @keyup="onChange">
        </v-text-field>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      search:'',
    }
    
  },
  methods: {
    onChange() {
      this.$emit("search", this.search)
    },
  }
}
</script>

<style>
 .v-text-field{
    width: 400px;
  }
  .v-select{
    width: 170px;
  }
  
</style>