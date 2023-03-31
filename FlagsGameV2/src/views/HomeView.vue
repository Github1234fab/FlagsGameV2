<template>
  <div class="container_flags">
    <div v-for="(infos, index) in flags" :key="index">
      <div class="country_name">{{ infos.translations.fra.common }}</div>
      <div v-if="infos.flags.png">
        <img class="flags" :src="infos.flags.png" alt="Image des drapeaux" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      flags: [],
    }
  },
  mounted() {
    axios
      .get('https://restcountries.com/v3.1/all')
      .then((response) => {
        this.flags = response.data
        console.log(this.flags)
      })
      .catch((error) => {
        console.log(error)
      })
  }
}
</script>
<style>
.container_flags {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}
.flags {
  height: 100px;
  width: 150px;
  border-radius: 10px;
  box-shadow: 0px 0px 8px -3px rgb(74, 72, 72);
  opacity: 0.8;
}
.flags:hover {
  opacity: 1;
}
.country_name {
  font-family: poppins;
  margin-bottom: 20px;
}
button {
  height: 100px;
  width: 100px;
}
</style>