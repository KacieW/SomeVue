<template>
<div>
  <div @click="hideform=!hideform">
    <h1 id="pagetitle">Pets Service</h1>
    <h2><span id="addBtn">+</span>Add Service For Your Pet</h2>
  </div>
  <div class="penal-body" :class="{hide:hideform}">
    <form @submit.prevent='requestAdd'>
      <div class="inputArea">
        <label>Pet Name</label>
        <input id="petname" v-model="formData.petName" type="text" placeholder="Pet's Name" />
      </div>
      <div class="inputArea">
        <label>Pet Age</label>
        <input id="petage" v-model="formData.petAge" type="text" placeholder="pet's age" />
      </div>
      <div class="inputArea">
        <label>Pet Gender</label>
        <input type="radio" class="radiobtn" v-model="formData.petGender" value="F"><label>F</label>
        <input type="radio" class="radiobtn" v-model="formData.petGender" value="M"><label>M</label>
        <!-- <input id="petgender" v-model="formData.petGender" type="text" placeholder="pet's gender" /> -->
      </div>
      <div class="inputArea">
        <label>Pet Service</label>
        <!-- <input id="petservice" type="text" placeholder="pet's service" /> -->
        <input type="radio" class="radiobtn" v-model="formData.petService" value="Grooming"><label>Grooming</label>
        <input type="radio" class="radiobtn" v-model="formData.petService" value="Training"><label>Traning</label>
        <input type="radio" class="radiobtn" v-model="formData.petService" value="Hotel"><label>Hotel</label>
      </div>
      <div class="inputArea">
        <label>Pet Appointment Date</label>
        <input type="text" id="petAptDay" v-model='formData.petAptDay' placeholder="mm-dd-yyyy" />
      </div>
      <div class="inputArea">
        <label>Pet Appointment time: {{timeData}}</label>
        <ul>
          <li class="sertime" v-for="(x, j) in petAptTime" :key='j' @click='requestTime(x, j); changeColor(x,j)'>
            {{x}}
          </li>
        </ul>
        <!-- <input id="petapt" type="text" placeholder="pet's appointment" /> -->
      </div>
      <div>
        <button id="submitPet" type="submit">Add Pet</button>
      </div>
    </form>
  </div>
</div>
</template>

<script>
import moment from 'moment';
export default {
  name: 'AddPet',
  data() {
    return{
      hideform:true,
      formData:{},
      timeData:'',
      dayData:''
    }
  },
  props:['petAptTime'],
  methods:{
    requestAdd:function(){
      console.log(this.formData);
      this.$emit('addRecord', this.formData);
      this.formData = [];
      this.hideform=true;
    },
    changeColor:function(val,j){
      var temp = j+1;
      document.querySelectorAll('.sertime').forEach((x)=>{
        x.style.background = '#fff';
      });
      var selectItem = document.querySelector('.sertime:nth-of-type('+temp+')');
      selectItem.style.background='#ffc082';
    },
    requestTime:function(val, j){
      this.timeData = val;
      this.formData.petAptDate = val;
      //this.$emit('removeTime', val, j);
    }
  }
}
</script>
<style scoped>
.hide{
  display:none;
}
#pagetitle{
  margin-bottom: 30px;
  font-size: 4em;
}
#addBtn{
  border: 1px solid #ffc082;
  border-radius: 50%;
  padding: 0 8px;
  margin-right: 6px;
  background: #ffc082;
}
.penal-body{
  margin: 40px auto;
}
form{
  width:40%;
  margin:auto;
}
.inputArea{
  text-align: left;
  margin: 10px 20px;
}
#petage{
  margin-left: 15px;
}
.sertime{
  display: inline-block;
  margin:10px;
  padding:4px 6px;
  border:1px solid #ffc082;
  border-radius: 2px;
}
#petname{
  margin-left: 2px;
}
input{
  line-height: 2.2em;
  width: 70%;
  padding-left: 6px;
  font-size: 12px;
}
.radiobtn{
  width:20px;
}
#submitPet{
  line-height: 2em;
  font-size: 14px;
  border-color: #42b983;
  border-radius: 4px;
  margin-top: 10px;
}
</style>
