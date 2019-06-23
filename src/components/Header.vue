<template>
  <div>
    <div id="header">
      <ul>
        <li>
          Photo App
        </li>

        <li>
          <button @click="openForm">add photo</button>
        </li>
        <li class="res">
          |||
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  methods:{
    openForm:function(){
      this.$emit('formVis', true)
    },

  },
  props: ['component']
}
</script>
<style scoped>

#header{
  width: 100%;
}

#header > ul {
    width:100%;
    padding:5px 0;
    margin:0;
}
#header > ul > li:first-child{
  display: inline-block;
}
#header > ul > li:not(:first-child){
    float: right;
    display:table-cell;
    white-space:nowrap;
}

#header > ul > li:last-child{
    overflow:hidden;
    border-right:none;
    text-align: right;
    float: right;
}
#header > ul > li.res{
  display: none;
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
</style>
