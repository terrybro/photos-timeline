<template>
  <div id="app">
    <Header @formVis="openForm"></Header>
    <Timeline :times="entries" @theDate="setDate"></Timeline>
    <Images :images="allImgs" @vis="openModal" @currIndex="setIndex"></Images>
    <Gallery :entry="currEntry" v-if="galleryVis" @vis="openModal"  @current="updateIndex" :imgIndex="imgIndex"></Gallery>
    <Upload v-if="uploadVis" @formVis='openForm'></Upload>
  </div>
</template>

<script>
import Header from './components/Header'
import Timeline from './components/Timeline'
import Images from './components/Images'
import Gallery from './components/Gallery'
import Upload from './components/Upload'

export default {
  name: 'App',
  components: {
    Header,
    Timeline,
    Images,
    Gallery,
    Upload
  },
  data () {
    return {
      imgIndex:0,
      galleryVis:false,
      uploadVis:false,
      currDate:"16/01/2014",
      entries:[
   {
      "entry":{
         "date":"16/01/2014",
         "longDate":"16th Jan 2014",
         "images":[
           {
             "url":"https://placeimg.com/600/600/people",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/any",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/nature",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           }

         ]
      }
   },
   {
      "entry":{
         "date":"28/02/2014",
         "longDate":"28th Feb 2014",
         "images":[
           {
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/arch",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           }

         ]
      }
   },
  {
      "entry":{
         "date":"17/03/2014",
         "longDate":"17th March 2014",
         "images":[
           {
             "url":"https://placeimg.com/600/600/people",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/animals",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },

         ]
      }
   },
   {
      "entry":{
         "date":"28/03/2014",
         "longDate":"28th Feb 2014",
         "images":[
           {
             "url":"https://placeimg.com/600/600/nature",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/any",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/nature",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/tech",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           },
           {
             "url":"https://placeimg.com/600/600/any",
             "title":"Holiday in France",
             "caption":"Got lost going to the Basilica of the Sacré-Coeur"
           }

         ]
      }
   }
]

    }
  },
  computed:{
    allImgs: function(){
        return this.entries.find(e => e.entry.date == this.currDate).entry.images
    },
    currEntry: function(){
        return this.entries.find(e => e.entry.date == this.currDate).entry
    }
  },
  methods:{
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
