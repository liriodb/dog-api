<template>
  <div class="images">
    <div class="image-content" v-for="(image, imageIndex) in paginatedData" :key="imageIndex">
        <img :src="image" class="image" :key="imageIndex" />
    </div>
    <div class="content-button" v-if="!showButton">
      <button @click="prevPage" :disabled="pageNumber == 0">
        Anterior
      </button>
      <button @click="nextPage" :disabled="pageNumber >= pageCount - 1">
        Siguiente
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'list',
  props: ['listImages'],
  data () {
    return {
      dataImages: [],
      pageNumber: 0,
      size: 2,
      showButton: true
    }
  },
  computed: {
    pageCount(){
      let sizeData = this.dataImages.length;
      let size = this.size;
      return Math.ceil(sizeData/size);
    },
    paginatedData(){
      let start = this.pageNumber * this.size;
      let end = start + this.size;
      return this.dataImages.slice(start, end);
    }
  },
  watch: {
    listData: function (val) {
      this.dataBreed = val;
    },
    listImages: function (val){ 
      this.showButton = false;
      this.dataImages = val;
    }
  },
  methods: {
    nextPage(){
      this.pageNumber++;
    },
    prevPage(){
      this.pageNumber--;
    }
  }
}
</script>

<style>
  button {
    background-color: #80808054;
    border: none;
    padding: 8px 20px;
  }
  button:first-child{
    margin-right: 10px;
  }
  button:disabled{
    background-color: #80808017;
  }
  .image-content {
    max-width: 225px;
    height: 225px;
    margin: 0 auto 20px auto;
    position: relative;
    overflow: hidden;
  }
  .image {
    width: auto;
    height: 100%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
  }
  .content-button {
    margin: 10px 0 20px;
  }
</style>
