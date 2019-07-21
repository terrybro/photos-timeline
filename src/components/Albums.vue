<template>
  <div>
    <div v-for="album in albums" id="icons">
    <img :src="album.icon" :data-id="album.album"  @click="setVis(album.album)" />
    <h3>{{album.album}}</h3>
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
    setVis: function(i){
      this.$emit('album', i)
    }
  },
  props: ['albums']
}

</script>


<style scoped>
#icons{
    display: inline-block;
    text-align: center;
    margin:44px;
}
img{
  width:90px;
}


</style>
