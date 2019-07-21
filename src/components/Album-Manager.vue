<template>
  <div class="form">

    <form v-on:submit.prevent="albumName()">
<h3 @click="close()">x</h3>
      <p>
        <label for="album">Add to an Existing Album</label>
      </p>
      <select id="album" name="albums" v-model="selected">
        <option>
          Choose an album
        </option>
        <option v-for="album in albums" :value="album.album">{{album.album}}</option>
      </select>
      <p>

      </p>
      <label for="fname">Or Create a New Album </label>
      <input type="text" id="fname" name="albumName" v-model="selected" @focus="clear()" >
      <div v-if="iconVis">
        <p>
          select an icon
        </p>
        <img src="../assets/bday.png" width="66px" @click="image"/>
        <img src="../assets/xmas.jpg" width="66px" @click="image"/>
        <img src="../assets/holiday.png" width="66px" @click="image"/>
      </div>


      <input type="submit" value="Add image to album">
</form>
  </div>
</template>

<script>

  export default {
    data () {
      return {
        selected:"Choose an album",
        iconVis:false
      }
    },
    methods:{
      clear:function(){
        this.selected = ""
        this.iconVis = true
      },
      image:function(img){
        this.$emit('image', img.srcElement.src)
      },
      albumName:function(){
        this.$emit('changeName', this.selected)
        this.$emit('albumFormVis')
      },
      close:function(){
        this.$emit('albumFormVis')
      }
    },
    props: ['albums']
  }
</script>
<style scoped>
h3{
  display: inline-block;
  float: right;
}
div{
  width:300px;
  margin: auto;
}
input[type=text], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=submit] {
  width: 100%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit]:hover {
  background-color: #45a049;
}

div .form {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}
img{
  display: inline-block;
  margin:8px 0;
}
</style>
