<template>
  <div>
    <div id="timeline">
      <ul>
        <li v-for="(date, index) in times" @click="setDate(date.entry.date, index)" :class="{ active : active_el == index }"  >
          {{date.entry.date}}
        </li>
      </ul>
      <div class="btn" @click="slide(-1)">
        <
      </div>
      <div class="btn btn-next" @click="slide(1)">
        >
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        active_el:0
      }
    },
    methods:{
      setDate:function(date, i){
        this.activate(i);
        this.$emit('theDate', date)
      },
      activate:function(el){
        this.active_el = el;
    }
    },
    props: ['times']
  }
</script>
<style scoped>
#timeline{
  white-space: nowrap;
  overflow: hidden;
  height:48px;
  position: relative;
}
.active {
  color:red;
  font-weight:bold;
}
.btn {
  color: #fff;
  background-color: #000;
  font-size: 12px;
  font-weight: bold;
  cursor: pointer;
  border: 2px solid #000;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 30px;
  height: 30px;
  position: absolute;
  top: 12px;
  left: 4px;
  transition: transform 0.3s ease-in-out;
  user-select: none;
}
.btn-next {
  left: auto;
  right: 4px;
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 6px 28px;
  overflow: hidden;
  background-color: #fff;
}

li {
  float: left;
    padding: 12px;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 16px;
  text-decoration: none;
}

li a:hover {
  background-color: #111111;
}

</style>
