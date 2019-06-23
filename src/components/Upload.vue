<template>
  <transition>
  <div v-if="show" :key="0">
    <form id="form">
      <div>
        <label>Add photo</label>
        <div>
          <input type="text" placeholder="Photo title">
          <p @click='show'>
            x
          </p>
        </div>
      </div>
      <div>
        <label>Caption</label>
        <div>
          <textarea rows="5" placeholder="Photo caption"></textarea>
        </div>
      </div>
      <div>
        <div>
          <button type="file">Select image</button><button type="submit" class="upload">Upload</button>
        </div>
      </div>
    </form>
  </div>
</transition>
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
#form{
  position: fixed;
  padding: 12px;
  top: 0;
  bottom: 0;
  left: 60%;
  right: 0;
  background-color: rgba(0, 0, 0, 0.9);
}
#form p{
  position: absolute;
  top: 22px;
  right: 44px;
  color: #fff;
}
#form button{
  padding: 6px
}
.slide {
  transition: all 0.5s;

}
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-enter {
  transform: translate(100%);
}
.slide-leave-to {
  transform: translate(-100%);
}
</style>
