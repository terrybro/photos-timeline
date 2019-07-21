<template>
  <div class="form" v-if="show" :key="0">
    <form>
        <label>Add photo</label>
                  <p @click='show'>x</p>
        <div>
          <input type="text" placeholder="Photo title">
        </div>
        <div>
          <input type="text" placeholder="Photo caption">
        </div>
          <select class="date">
            <option value="">01</option>
            <option value="">Month</option>
            <option value="">Year</option>
          </select>
          <select class="date">
            <option value="">01</option>
            <option value="">Month</option>
            <option value="">Year</option>
          </select>
          <select class="date">
            <option value="">2019</option>
            <option value="">Month</option>
            <option value="">Year</option>
          </select>

      <div>

          <button type="file">Select Image</button>
          <input type="submit" value="Load Photo">

      </div>
    </form>
  </div>
</template>

<script>
  export default {
    data () {
      return {

      }
    },
    methods:{
      show:function(){
        this.$emit('formVis')
      }
    },
    props: []
  }
</script>
<style scoped>
.date option{
  display: inline;
  width: 30px;
}
p{
  width: 34px;
  float: right;
  text-align: right;
}
#form{
  position: fixed;
  padding: 12px;
  top: 200px;
  left: 60%;
  right: 0;
}
input[type=text], select, button {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=submit], button {
  width: 100%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit], button:hover {
  background-color: #45a049;
}

div .form {
  width: 50%;
  margin: auto;
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}
.date option{
  display: inline;
  width: 30px;
}

</style>
