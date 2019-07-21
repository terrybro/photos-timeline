<template>
  <div id="app">
    <Header @formVis="openForm" v-model='search' @input="search = $event"  @section="setVis" @albumFormVis="closeAlbum" @upload="uploadVis = true"></Header>
    <Timeline v-if="timelineVis" :dates="uniqueDates()" @theDate="setDate"></Timeline>
    <Images v-if="imagesVis" :currSection="currSection" :images="filterImages()" @vis="openModal" @currIndex="setIndex" @setCurrImage="setImage" @contextMenu="openContext"></Images>
    <contextMenu v-if="menuVis" @openAlbumManager="albumManager"></contextMenu>
    <albumManager v-if="albumManagerVis" :albums="albums" @albumFormVis="closeAlbum" @changeName="changeAlbumName" @image="addImage"></albumManager>
    <Albums v-if="albumVis" :albums="albums"  @album="setAlbumVis" ></Albums>
    <Gallery v-if="galleryVis" @vis="openModal"  @current="updateIndex" :imgIndex="imgIndex" :images="filterImages()"></Gallery>
    <transition name="slide-fade">
      <Upload v-if="uploadVis" @formVis='openForm'></Upload>
    </transition>
  </div>
</template>

<script>
import Header from './components/Header'
import Timeline from './components/Timeline'
import Images from './components/Images'
import Gallery from './components/Gallery'
import Albums from './components/Albums'
import Upload from './components/Upload'
import AlbumManager from './components/Album-Manager'
import contextMenu from './components/Context-Menu'

const xmas = require('./assets/xmas.jpg')
const bday = require('./assets/bday.png')
const hols = require('./assets/holiday.png')
//import imageData from './data.js'

export default {
  name: 'App',
  components: {
    Header,
    Timeline,
    Images,
    Gallery,
    Upload,
    Albums,
    AlbumManager,
    contextMenu
  },

  data () {
    return {
      search:'',
      albumIndex:0,
      albumName:"",
      imgIndex:0,
      albumVis:false,
      albumManagerVis:false,
      imagesVis:true,
      timelineVis:true,
      galleryVis:false,
      uploadVis:false,
      currDate:"16/01/2014",
      currAlbum:"",
      currImage:{},
      currSection:0,
      tempImage:{},
      menuVis:false,
      images:[
           {
             "id":1,
             "url":"https://placeimg.com/600/600/nature?11",
             "title":"Holiday in Paris",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["paris"],
             "date":"16/01/2014",
             "album":"holiday",
             "icon" : hols
           },
           {
             "id":2,
             "url":"https://placeimg.com/600/600/nature?1",
             "title":"Holiday in Paris",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/01/2014",
             "album":"xmas",
             "icon" : xmas
           },
           {
             "id":3,
             "url":"https://placeimg.com/600/600/tech?22",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/01/2014",
             "album":"xmas"
           },
           {
             "id":4,
             "url":"https://placeimg.com/600/600/nature?33",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"17/01/2014",
             "album":"xmas",
             "icon" : xmas
           },
           {
             "id":5,
             "url":"https://placeimg.com/600/600/people?31",
             "title":"Holiday in London",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"17/01/2014",
             "album":"xmas",
             "icon": xmas
           },
           {
             "id":6,
             "url":"https://placeimg.com/600/600/any?44",
             "title":"Holiday in London",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/03/2014",
             "album":"birthday",
             "icon" : bday
           },
           {
             "id":7,
             "url":"https://placeimg.com/600/600/any?41",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/03/2014",
             "album":"birthday"
           },
           {
             "id":8,
             "url":"https://placeimg.com/600/600/any?92",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/03/2014",
             "album":""

           },
           {
             "id":9,
             "url":"https://placeimg.com/600/600/any?43",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"26/05/2014",
             "album":""
           },
           {
             "id":10,
             "url":"https://placeimg.com/600/600/any?45",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"26/05/2014",
             "album":""
           },
           {
             "id":11,
             "url":"https://placeimg.com/600/600/any?46",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"27/05/2014",
             "album":""
           },
           {
             "id":12,
             "url":"https://placeimg.com/600/600/any?47",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"27/05/2014",
             "album":""
           },
           {
             "id":13,
             "url":"https://placeimg.com/600/600/any?48",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"27/05/2014",
             "album":""
           },
           {
             "id":14,
             "url":"https://placeimg.com/600/600/any?49",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/06/2014",
             "album":""
           },
           {
             "id":15,
             "url":"https://placeimg.com/600/600/nature",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"17/06/2014",
             "album":""
           },
           {
             "id":16,
             "url":"https://placeimg.com/600/600/people",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/06/2014",
             "album":""
           },
           {
             "id":17,
             "url":"https://placeimg.com/600/600/any",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/06/2014",
             "album":""
           },
           {
             "id":18,
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/06/2014",
             "album":""
           },
           {
             "id":19,
             "url":"https://placeimg.com/600/600/nature",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"17/06/2014",
             "album":""
           },
           {
             "id":20,
             "url":"https://placeimg.com/600/600/people",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/06/2014",
             "album":""
           },
           {
             "id":21,
             "url":"https://placeimg.com/600/600/any",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/07/2014",
             "album":""
           },
           {
             "id":22,
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur",
             "tags":["holiday"],
             "date":"16/07/2014",
             "album":""
           },

         ]
    }
  },
  computed: {
    filteredList() {
      return this.images.filter(image => {
        return image.title.toLowerCase().includes(this.search.toLowerCase())
      })
    },
    albums(){
      return this.images.filter(function(image, index, self) {
          if (Object.keys(image.album).length > 0)  {return index == self.map(res => res.album).indexOf(image.album)};
        });
  }
  },
  methods:{
    setImage:function(image){
      this.currImage = image;
    },
    test:function(){
      console.log(this.images[0].album)
      this.images[6].album = "hell"
    },
    albumTemp:function(image){
      const index = this.images.map(e => e.id).indexOf(image.id);
      this.images[index].album = this.albumName
    },
    changeAlbumName:function(name){
      this.currImage.album = name
      this.setVis(2)
    },
    addImage:function(icon){
            this.currImage.icon = icon
    },
    album:function(){
      this.albumManagerVis = true;
    },
    filterImages: function(){
      switch (true)
      {
        case this.currSection == 0:
            return this.timeline();
            break;

        case this.currSection == 2:
            return this.albumList();
            break;

        case this.currSection == 1:
            return this.filteredList;
            break;
    }
  },
    uniqueDates: function() {
      return this.images.filter((image, index, arr) => {
      return arr.map(mapObj => mapObj["date"]).indexOf(image["date"]) === index;
    });
  },
    albumList: function() {
      return  this.images.reduce((filtered, image) => {
        if (image.album && image.album === this.currAlbum) {
          filtered.push(image);
        }
        return filtered;
      }, []);
    },
    timeline: function() {
      return  this.images.reduce((filtered, image) => {
        if (image.date == this.currDate) {
          filtered.push(image);
        }
        return filtered;
      }, []);
    },
    openModal: function(value){
      this.galleryVis = value
    },
    setIndex: function(value){
      this.imgIndex = value
    },
    setDate: function(value){
      this.currDate = value
    },
    updateIndex: function(value){
      this.imgIndex = value
    },
    openForm: function(value){
      this.uploadVis = !this.uploadVis
    },
    setAlbumVis: function(i){
      this.currAlbum = i;
      this.albumVis = false;
      this.imagesVis = true;
    },
    setVis: function(i){
      this.currSection = i;
      if (i === 0){
        this.timelineVis = true;
        this.imagesVis = true;
        this.albumVis = false;
      };
      if (i === 1){
        this.timelineVis = false;
        this.imagesVis = true;
        this.albumVis = false;
      };
      if (i === 2){
        this.timelineVis = false;
        this.imagesVis = false;
        this.albumVis = true
      }
    },
    albumManager:function(){
      this.albumManagerVis = true;
      this.closeMenu();
    },
    closeMenu:function(){
      this.menuVis =  false;
    },
    closeAlbum:function(){
      this.albumManagerVis =  false;
    },
    openContext:function(){
      this.menuVis = true;
    }

  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s ease;
}
.slide-fade-enter, .slide-fade-leave-to {
  opacity: 0;
}

/* Mobile Styles */
@media only screen and (max-width: 400px) {
  body {
    background-color: #F09A9D; /* Red */
  }
}

/* Tablet Styles */
@media only screen and (min-width: 401px) and (max-width: 960px) {
  body {
    background-color: #F5CF8E; /* Yellow */
  }
}

/* Desktop Styles */
@media only screen and (min-width: 961px) {
  body {
    background-color: #B2D6FF; /* Blue */
  }
}
#header{
  color: #eee;
  padding: 8px;
  background-color: #000;
}

#close{
  display: inline-block;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
}
</style>
