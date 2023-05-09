<template>
  <div class="container_homePage">
    
    <div class="title"></div>
    <!-- <h1>Connais-tu ce monde?</h1> -->
  </div>
  <!-- <div class="container_flags">
    <div v-for="(infos, index) in flags" :key="index">
      <div class="country_name">{{ infos.translations.fra.common }}</div>
      <div v-if="infos.flags.png">
        <img class="flags" :src="infos.flags.png" alt="Image des drapeaux" />
      </div>
    </div>
  </div> -->
</template>
<script>
import axios from 'axios'
export default{
  data() {
  
    return {
      flags: []
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
  height: 20px;
  width: 20px;
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
a{
  text-decoration: none;
}

.container_homePage {
  display: flex;
  height: 100vh;
  width: 100%;
  background: url('../assets/_65af0787-f768-43b3-8750-ca3315853ea0.jpeg');
  background-size: cover;
  position: relative;
}

.container_menu {
  width: 100%;
  display: flex;
  justify-content: space-around;
  height: 300px;
  margin-top: 50px;

}

.container_homePage h1{
 position: absolute;
  top: 5%;
  left: 30%;
  color: white;
  font-family: oswald;
}

</style>
