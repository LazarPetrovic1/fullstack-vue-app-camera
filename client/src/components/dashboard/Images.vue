<template lang="html">
  <div class="container">
    <h1 class="text-center">Recently taken images</h1>
    <div class="d-flex flex-row flex-wrap">
      <img v-for="img in imgs" :src="imageLink(img)" :title="img" class="image">
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "Images",
  data() {
    return {
      imgs: null
    }
  },
  mounted() {
    const getImages = async () => {
      const res = await axios.get("http://localhost:5000/api/auth/images")
      this.imgs = await res.data.images
      await console.log(res.data.images)
    }
    getImages()
  },
  methods: {
    imageLink(img) {
      return require(`../../assets/images/${img}`)
    }
  }
}
</script>

<style lang="css" scoped>
.image {
  max-width: 500px;
  margin: 10px;
  cursor: pointer;
}
</style>
