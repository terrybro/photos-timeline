<template>
  <div>
    <div id="main">
      <div>
        <img v-for="(image, index) in images " :src="image.url" @click="modalVis(index)" @contextmenu.prevent="openMenu($event, image)">
      </div>
    </div>
  </div>
</template>

<script>

import EventBus from '../event-bus';

export default {
  name: 'Images',
  data () {
    return {
      pages:10,
      menuVis:false,
      albumManagerVis:false
  }
},
  computed:{
    pageCount(){
      let l = this.images.length,
      s = this.pages;
      return Math.floor(l/s);
    },
    paginatedData(){
      const start = this.pageNumber * this.size,
      end = start + this.size;
      return this.listData.slice(start, end);
    }
  },
  methods:{
    openMenu:function(event, image){
      if(this.currSection == 0 || 1 && image.album == ""){
        event.target.classList.add('red')
        this.$emit('contextMenu')
        this.$emit('setCurrImage', image)
      }
    },
    modalVis:function(i){
      this.$emit('vis', true)
      this.$emit('currIndex', i)
    }

  },
  props:['images', 'vis', 'currSection']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#main div{
  display: inline;
}
#main img{
  width: 80px;
  cursor: pointer;
}
.red{
  border: solid 4px red;
}
</style>
