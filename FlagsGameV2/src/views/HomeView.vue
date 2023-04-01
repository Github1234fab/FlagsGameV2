<template>
  <div class="container_homePage">
    <h2 class="game_menu">Cherchez le nom des drapeaux des pays du monde entier!</h2>
    <img
      class="background_img"
      src="https://media.istockphoto.com/id/492528693/fr/photo/domaine-de-leurope-la-nuit.jpg?s=612x612&w=0&k=20&c=Ua5kSJPvLb-pFae_6jd3-FyNTHNWaoQcT0-PXbXIOiA="
      alt=""
    />
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
export default {
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
.background_img {
  height: 100vh;
  width: 100%;
}
.game_menu {
  width: 200px;
  font-family: poppins;
  font-size: 24px;
  color: rgb(255, 255, 255);
  position: absolute;
  top: 50px;
  left: 100px;
  text-shadow: 
  0px 0px 10px #ffffff,
   0px 0px 42px #fff,
    0px 0px 77px #a9a9f6,
      0px 0px 100px #3e75f6;
      /* background-size: cover;
      background-position: center;
      background-clip: text;
      -webkit-background-clip: text;
      background-image: url("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQTixK_AMiyslawcC7dmv2_9swZqpcdxnkDsw&usqp=CAU");
} */
}
.container_homePage {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
}
</style>
