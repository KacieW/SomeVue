<template>
  <li>
    <div>
      <span>Name: {{listItme.petName}}</span>
      <button
        @click="requestRemoval"
      >x</button>
    </div>
    <div>Age:{{listItme.petAge}}</div>
    <div>Gender:{{listItme.petGender}}</div>
    <div>Service:{{listItme.petService}}</div>
    <div>Apt Day:{{listItme.petAptDay}}</div>
    <div>Apt Time:{{listItme.petAptDate}}</div>
  </li>
</template>

<script>
export default{
  name:'petListItem',
  props:['listItme'],
  methods:{
    requestRemoval:function(){
      this.$parent.$emit('remove', this.listItme);//go up 2 level
    }
  }
}
</script>
<style scoped>
button{
    padding: 2px 6px 4px;
    border: none;
    border-radius: 2px;
    background: #ffc082;
    float: right;
}
li{
  width: 80%;
    margin: auto;
}
li div{
  margin: auto 16px;
}
</style>
