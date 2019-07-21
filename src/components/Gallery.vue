<template>
  <div id="modal">
    <transition-group tag="div" :name="transitionName">
      <div id="gallery" v-if="show" :key="imgIndex" class="slide">
        <h1 v-if="captions" class="legend title">{{`${images[imgIndex].title}`}}</h1>
        <h3  v-if="captions" class="legend caption">{{`${images[imgIndex].caption}`}}</h3>
        <img :src="`${images[imgIndex].url}`"  />
      </div>
    </transition-group>
    <div class="btn" @click="slide(-1)"><</div>
    <div class="btn btn-next" @click="slide(1)">></div>
    <button @click="close" class="btn btn-close">x</button>
    <input type="checkbox" id="one" @click="toggle"/><label for="one">No captions</label>
  </div>
</template>

<script>
export default {
  name: 'Gallery',
  data () {
    return {
      currDate:"16/01/2014",
      current: 0,
      direction: 1,
      transitionName: "fade",
      show: true,
      captions:true
    }
  },
  props:["imgIndex", "images"],
  computed:{

  },
  methods:{
    toggle:function(){
      this.captions = !this.captions;
    },
    slide(dir) {
     this.direction = dir;
     dir === 1
       ? (this.transitionName = "slide-next")
       : (this.transitionName = "slide-prev");
     var len = this.images.length;
     let newIndex = (this.imgIndex + dir % len + len) % len;
     this.$emit('current', newIndex)
   },
    close: function(event){
      this.$emit('vis', false)
    }
  }
}
</script>
<style scoped>
img{
  width:600px;
}
input, label{
  position: absolute;
  top: 22px;
  right: 4%;
  color: #fff;
}
label{
  padding-right: 22px;
  top:20px;
}
.legend{
  position: absolute;
  text-align: center;
  background-color: #fff;
  color: #000;

}
.title{
  top:50px;
}
.caption{
  bottom:50px;
}
#modal{
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.9);
  justify-content: center;
  align-items: center;
  display: flex;
}
#slider {
  width: 100%;
  height: 100vh;
  position: relative;
}

.slide {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* FADE IN */
.fade-enter-active {
  transition: opacity 1s;
}
.fade-enter {
  opacity: 0;
}

/* GO TO NEXT SLIDE */
.slide-next-enter-active,
.slide-next-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-next-enter {
  transform: translate(100%);
}
.slide-next-leave-to {
  transform: translate(-100%);
}

/* GO TO PREVIOUS SLIDE */
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-prev-enter {
  transform: translate(-100%);
}
.slide-prev-leave-to {
  transform: translate(100%);
}

.btn {
  color: #fff;
  font-size: 22px;
  font-weight: bold;
  z-index: 10;
  cursor: pointer;
  border: 3px solid #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70px;
  height: 70px;
  position: absolute;
  top: calc(50% - 35px);
  left: 1%;
  transition: transform 0.3s ease-in-out;
  user-select: none;
}
.btn-next {
  left: auto;
  right: 1%;
}
.btn-close{
  color: #000;
  top: 20px;
  right: 10px;
  width: 30px;
  height: 30px;
}

</style>
