<template lang="html">
  <div id="sidebar">
    <div>

      <h2>Find the perfect pint...</h2>
      <div class="select-container">
        <h3>Country</h3>
        <field-select
        :allFields="allCountries"
        field="country"
        displayField="countries"/>
      </div>

      <div class="select-container" v-if='allCategories.length > 0'>
        <h3>Category</h3>
        <field-select
        :allFields="allCategories"
        field="cat_name"
        displayField="categories"/>
      </div>

      <div class="select-container" v-if='allStyles.length > 0'>
        <h3>Style</h3>
        <field-select
        :allFields="allStyles"
        field="style_name"
        displayField="styles"/>
      </div>

      <div class="select-container">
        <h3>Brewery</h3>
        <field-select
        :allFields="allBreweries"
        field="name_breweries"
        displayField="breweries"/>
      </div>

      <a id='random-beer' v-on:click="randomBeer"><i class="fas fa-random"> </i> Random Beer </a>

    </div>
    <h4 id="listing-count">Currently listing {{ numOfBeers }} beers from {{ allCountries.length }}
      <span v-if="allCountries.length===1">country</span>
      <span v-if="allCountries.length > 1">countries</span>
    </h4>
  </div>
</template>

<script>
import FieldSelect from './FieldSelect.vue'
import { eventBus } from '../main.js'

export default {
  name: 'sidebar',
  props: [ 'allCountries', 'allStyles', 'allCategories', 'allBreweries', 'numOfBeers', 'filteredBeers' ],
  components: {
    'field-select': FieldSelect
  },
  methods: {
    randomBeer: function() {
      let randomIndex = Math.floor(Math.random() * this.filteredBeers.length)
      let randomBeer = this.filteredBeers[randomIndex]
      eventBus.$emit('random-beer', randomBeer)
    }
  }
}
</script>

<style lang="css" scoped>

#sidebar {
  display: flex;
  flex-direction: column;
  background-color: #E0DFD5;
  grid-area: sidebar;
  justify-content: space-between;
}

.select-container {
  margin: 3vw 0;
}

h2 {
  font-family: 'Lobster', cursive;
  margin: 2vw 0vw;
  font-size: 2rem;
  color: #F06543;
}

#listing-count {
  margin-bottom: 4vw;
}

#random-beer {
  font-size: 1.5rem;
  font-weight: bold;
}

#random-beer:hover {
  color: #F06543;
  cursor: pointer;
}

</style>
