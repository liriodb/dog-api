<template>
  <div id="app">
    <img alt="Api logo" src="https://dog.ceo/img/dog-api-logo.svg">
    <h1>Dog Breeds:</h1>
    <api :nameBreed="nameBreed" @getbreedslist="getBreedsList($event)" @getimageslist="getImagesList($event)"/>
    <list :listData="listData" @sendnamebreed="getNameBreed($event)"/>
    <images :listImages="listImages"/>
  </div>
</template>

<script>
import api from './components/api.vue'
import list from './components/list.vue'
import images from './components/images.vue'

export default {
  name: 'app',
  components: {
    api,
    list,
    images
  },
  data () {
    return {
      listData: {},
      nameBreed: '',
      listImages: []
    }
  },
  methods: {
    getBreedsList(getList){
      this.listData = getList;
    },
    getNameBreed(getName){
      this.nameBreed = getName;
    },
    getImagesList(images) {
      this.listImages = images;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-size: 1.5em;
  margin: 24px 0;
}
</style>
