<template>
  <div>
    <div id="main">
      <div>
        <img v-for="(image, index) in images" :src="image.url" @click="changeVis(index)">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Images',
  data () {
    return {

    }
  },
  props:['images', 'vis'],
  computed:{

  },
  methods:{
    changeVis:function(index){
      console.log(index)
      this.$emit('vis', true)
      this.$emit('currIndex', index)

    }
  }
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
</style>
