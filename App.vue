<template>
  <div id="main-app">
    <!-- <add-pet @addRecord='addPet' :petAptTime = 'aptTime' @removeTime='removeTime' ></add-pet> -->
    <add-pet @addRecord='addPet' :petAptTime = 'aptTime'></add-pet>
    <search-pet @searchRecords = 'searchPets'
      :myKey = "filterKey"
      :myDir = "filterDir"
      @keyChange="changeKey"
      @dirChange="changeDir"></search-pet>
    <pet-list :petlists='filteredPets' @remove = 'removeItem'></pet-list>
  </div>
</template>

<script>
import moment from 'moment';
import PetList from './PetList.vue';
import AddPet from './AddPet.vue';
import SearchPet from './SearchPet.vue';
import _ from 'lodash';

var allPets = [{
    "petName": "Adam",
    "petAge": 3,
    "petGender":"F",
    "petService":"Hotel",
    "petAptDate":'10:00',
    "petAptDay":'11-16-2017'
  },
  {
    "petName": "Bill",
    "petAge": 1,
    "petGender":"F",
    "petService":"Grooming",
    "petAptDate":'16:00',
    "petAptDay":'10-10-2018'
  },
  {
    "petName": "Clark",
    "petAge": 9,
    "petGender":"F",
    "petService":"Training",
    "petAptDate":'9:00',
    "petAptDay":'04-02-2018'
  },
  {
    "petName": "Delit",
    "petAge": 2,
    "petGender":"M",
    "petService":"Grooming",
    "petAptDate":'13:00',
    "petAptDay":'03-21-2018'
  }
];

export default {
  name: 'app',
  data() {
    return {
      allPets: allPets,
      searchTerms : '',
      filterKey:'petName',
      filterDir:'asc',
      aptTime:['09:00','10:00','11:00', "12:00", '13:00']
    }
  },

  methods:{
    addPet:function(p){
      this.allPets.push(p);
    },
    removeItem:function(pI){
      this.allPets = _.without(this.allPets, pI);
    },
    //removeTime:function(pt, j){
      // this.aptTime = _.without(this.aptTime, pt);
      // if(pt!==''){
      //   this.aptTime.splice(j,0,pt);
      // }
    //},
    searchPets:function(terms){
      this.searchTerms = terms;
    },
    changeKey:function(v){
      this.filterKey =v;
    },
    changeDir:function(v){
      this.filterDir=v;
    }
  },
  computed:{
    searchedPets:function(){
      return this.allPets.filter((x)=>{
        return (
          (x.petName.toLowerCase().match(this.searchTerms.toLowerCase()))||
          (x.petAge.toString().match(this.searchTerms))
        )
      })
    },
    filteredPets:function(){
      return _.orderBy(this.searchedPets, (x)=>{
        console.log(x[this]);
        return x[this.filterKey];
      }, this.filterDir);
    }
  },

  components:{
    'pet-list':PetList,
    'search-pet':SearchPet,
    'add-pet':AddPet
  }//component register
}
</script>

<style>
#main-app{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
.activeTime{
  background: #ffc082;
}
#app li {
  text-align: left;
  padding: 10px;
  border-top: 1px solid gray;
}
a {
  color: #000;
}
</style>
