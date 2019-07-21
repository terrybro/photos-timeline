<template>
  <div>
    <div id="header">
      <ul>
        <li v-for="(item, index) in items" :class="{active: active == index}" @click="activeHeader(index)">
          {{item}}
        </li>
        <li v-if="active == 1">
          Search   <input type="text" width="42px"  ref="filter" v-model="searchVal" class="searchBox" @blur="clearText"/>
        </li>
        <li @click="upload">
          Add Photo
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import EventBus from '../event-bus';
export default {
  data() {
    return {
      active:0,
      isActive: false,
      searchVal:this.value,
      items:["Timeline", "All Images", "Albums"]
    }
  },
  methods:{
    upload:function(){
      this.$emit('upload')
    },
    clearText:function(event){
    event.target.value=''
    },
    activeHeader:function(i){
      this.active = i
      this.$emit('section', i)
      if(i == 0 || 1){
        this.$emit('albumFormVis')
      }
    },
    searchit:function(){
      console.log(this.value)
    },
    openForm:function(){
      this.$emit('formVis', true)
    },
    toggleTimeline:function(){
      this.$emit('toggle')
    },
    toggleSearch:function(){
      this.isActive = !this.isActive
      this.toggleTimeline()
      this.$refs.filter.focus()
    }
  },
  watch: {
    searchVal(val) {
      this.$emit('input', val);
    }
  },
  props: ['value']
}

</script>
<style scoped>

#header{
  width: 100%;
  height:66px;
  font: normal 23px/150% Arial, Helvetica, sans-serif;
}

#header > ul {
    width:100%;
    padding:5px 0;
    margin:0;
}
#header > ul li {
  display: inline-block;
  padding-right: 32px;
}

#header > ul > li.res{
  display: none;
}
.searchBox {
    width: 100%;
    font-size: 18px;
    border-radius: 6px;
    border: 1px #000 solid;
    padding: 4px 8px 4px;
}
li:last-child{
  float: right;
}
li{
  transition: all 0.5s;
}
li .active{
  color:red;
  transform: scale(1.5);
}
input[type=text] {
  width: 100px;
    transition: width 0.4s ease-in-out;
}
input[type=text]:focus {
  width: 200px;
}

button {
    width: 64px;
    padding:4px;
    cursor: pointer;
}
@media screen and (max-width: 400px) {
  #header > ul > li:not(:first-child){
    display: none;
  }
  #header > ul > li.res{
    display:inline-block;
  }
}
.res{
  font-weight: bold;
}
.active{
  color: red;
}
</style>
