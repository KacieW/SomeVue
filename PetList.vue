<template>
  <div id="app">
    <ul>
      <pet-list-item v-for="(item, i) in petlists" :key="i"
        :listItme ="item"></pet-list-item>
    </ul>
  </div>
</template>

<script>
import PetListItem from './PetListItem.vue'

export default{
  name:'petList',
  props:['petlists'],
  components:{
    'pet-list-item':PetListItem
  }
}
</script>
