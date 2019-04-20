<template>
  <div class="api"></div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'api',
  props: ['nameBreed'],
  data () {
    return {
      url: ''
    }
  },
  watch: {
    nameBreed: function (name) {
      this.url = name;
      this.getBreedImages();
    }
  },
  created: function(){
    this.getBreedsList();
  },
  methods: {
    getBreedsList(){
      let self = this;
      let response;
      axios.get('https://dog.ceo/api/breeds/list/all')
      .then(function (response) {
        response = response.data.message;
        self.sendBreed(response);
      })
      .catch(function (error) {
        console.log('Error: ' + error);
      });
    },
    getBreedImages() {
      let self = this;
      let responseImage;
      axios.get(`https://dog.ceo/api/breed/${self.url}/images`)
      .then(function (response) {
        responseImage = response.data.message;
        self.sendImages(responseImage)
      })
      .catch(function (error) {
        console.log('Error: ' + error);
      });
    },
    sendBreed(list) {
      this.$emit('getbreedslist', list);
    },
    sendImages(imageList) {
      this.$emit('getimageslist', imageList);
    }
  }
}
</script>
