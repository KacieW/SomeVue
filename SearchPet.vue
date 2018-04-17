<template>
  <div>
    <input v-model="searchTerm" type="text" id="searchTermBox" placeholder="Search"/>
    <div>
      <!--<button type="button" data-toggle="dropdown">Sort By</button>-->
      <span>Sort by: </span>
      <ul id="sortDir">
        <li><a href="#" @click="requestKeyChange('petName')">
          <span v-if="myKey==='petName'" class="choosen">Pet Name</span>
          <span v-else class="notchoosen">Pet Name</span>
        </a></li>
        <li><a href="#"
          @click="requestKeyChange('petGender')">
          <span v-if="myKey==='petGender'" class="choosen">Pet Gender</span>
          <span v-else class="notchoosen">Pet Gender</span>
        </a></li>
        <li><a href="#"
          @click="requestKeyChange('petAge')">
          <span v-if="myKey==='petAge'" class="choosen">Pet Age</span>
          <span v-else class="notchoosen">Pet Age</span>
        </a></li>
        <li><a href="#"
          @click="requestKeyChange('petService')">
          <span v-if="myKey==='petService'" class="choosen">Pet Service</span>
          <span v-else class="notchoosen">Pet Service</span>
        </a></li>
        <li><a href="#"
          @click="requestKeyChange('petAptDay')">
          <span v-if="myKey==='petAptDay'" class="choosen">Pet Apt Day</span>
          <span v-else class="notchoosen">Pet Apt Day</span>
        </a></li>
        <li><a href="#"
          @click="requestKeyChange('petAptDate')">
          <span v-if="myKey==='petAptDate'" class="choosen">Pet Apt Time</span>
          <span v-else class="notchoosen">Pet Apt Time</span>
        </a></li>
        <li role="separator">|</li>
        <li><a href="#"
          @click="requestDirChange('asc')">
          <span v-if="myDir==='asc'" class="choosen">Asc</span>
          <span v-else class="notchoosen">Asc</span>
        </a></li>
        <li><a href="#"
          @click="requestDirChange('desc')">
            <span v-if="myDir==='desc'" class="choosen">Dsc</span>
            <span v-else class="notchoosen">Dsc</span>
          </a></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default{
  name:'SearchPet',
  data(){
    return {
      searchTerm:''
    }
  },
  props:['myKey','myDir'],
  methods:{
    requestKeyChange:function(val){
      this.$emit('keyChange', val);
    },
    requestDirChange:function(val){
      this.$emit('dirChange', val)
    }
  },
  watch:{
    searchTerm:function(){
      this.$emit('searchRecords', this.searchTerm);
    }
  }
}
</script>
<style>
#searchTermBox{
  line-height: 2em;
  width: 35%;
  padding-left: 10px;
  font-size: 16px;
  margin-top: 40px;
}
.notchoosen{
  background:none;
}
.choosen{
  border-bottom:2px solid #ffc082;
  color:#42b983;
}
#sortDir, #sortDir li{
  display: inline-block;
}
#sortDir li{
  margin: 0 5px;
}
#sortDir a{
  text-decoration: none;
}
</style>
