<template>
  <div class="list">
    <select class="select" v-model="breedSelected">
      <option disabled value="">Selecciona una raza</option>
      <option v-for="(subBreed, breed, index) of dataBreed" :key="index">{{breed}}</option>
    </select>
    <select class="select" v-model="subBreedSelected">
      <option disabled value="">Selecciona una sub-raza</option>
      <option v-for="(subBreed, index) in dataSubBreed" :key="index">{{subBreed}}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'list',
  props: ['listData'],
  data () {
    return {
      dataBreed: [],
      dataSubBreed: [],
      breedSelected: '',
      subBreedSelected: '',
      nameBreed: ''
    }
  },
  watch: {
    listData: function (val) {
      this.dataBreed = val;
    },
    breedSelected: function (val) {
      this.pageNumber = 0;
      let nameSubBreed = this.dataBreed[val];
      if(nameSubBreed.length > 0) {
        this.dataSubBreed = nameSubBreed;
      }else{
        this.dataSubBreed = [];
      }
      this.nameBreed = val;
      this.getNameBreeds(this.nameBreed);
    },
    subBreedSelected: function (val) {
      this.pageNumber = 0;
      let nameSubBreed = `${this.nameBreed}/${val}`;
      this.getNameBreeds(nameSubBreed);
    }
  },
  methods: {
    getNameBreeds(name) {
      this.$emit('sendnamebreed', name);
    },
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
  .content-breeds{
    display: flex;
    flex-direction: column;
  }
  label {
    font-weight: bold;
  }
  .select {
    background-color: #80808054;
    padding: 5px;
    display: flex;
    margin: 0 auto 20px;
  }
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
