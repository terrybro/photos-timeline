<template>
    <div class="timeline">
        <div v-for="(date, id) in dates" @click="setDate(date.date, id)" class="date" :class="{ active : active_el == id }"  >
          <span>{{date.date}}</span>
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
    props: ['dates']
  }
</script>

<style scoped>
span{
  cursor: pointer;
}
.timeline{
  color: white;
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  cursor: ew-resize;
}
.timeline .date{
  flex: 0 0 auto;
}
.date{
  border: 2px solid red;
  padding: 4px;
  width: 150px;
  background: black;
}
.timeline {
  height: 48px;
  width: 100%;
  -webkit-overflow-scrolling: touch;
}
.timeline::-webkit-scrollbar { width: 0 !important }

.active {
  color:red;
  font-size: 110%;
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
