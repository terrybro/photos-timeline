<template>
  <div>
    <ul id="right-click-menu">
           <li @click="openAlbumManager">Add selected images to an album</li>
       </ul>
  </div>
</template>

<script>

export default {
  data () {
    return {

    }
  },
  methods:{
    openAlbumManager: function(){
      this.$emit('openAlbumManager')
    }
  }
}

</script>
<style scoped>
div{
  font-style: helvetica;
  text-align: center;
  font-size: 22px;
  width: 202px;
  height: 88px;
  margin: auto;
}

#right-click-menu{
    background: #FAFAFA;
    border: 1px solid #BDBDBD;
    box-shadow: 0 2px 2px 0 rgba(0,0,0,.14),0 3px 1px -2px rgba(0,0,0,.2),0 1px 5px 0 rgba(0,0,0,.12);
    display: block;
    list-style: none;
    margin: 0;
    padding: 0;
    position: absolute;
    width: 250px;
    z-index: 999999;
}

#right-click-menu li {
    border-bottom: 1px solid #E0E0E0;
    margin: 0;
    padding: 12px;
}

#right-click-menu li:last-child {
    border-bottom: none;
}

#right-click-menu li:hover {
    background: #1E88E5;
    color: #FAFAFA;
}

</style>
