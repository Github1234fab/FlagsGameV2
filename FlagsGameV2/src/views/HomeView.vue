<template>
  <div class="container_homePage">
    <div class="menu">
      <h2 class="game_menu">Chercher le nom des drapeaux du monde entier</h2>
    </div>
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
import axios from "axios";
export default {
  data() {
    return {
      flags: [],
    };
  },
  mounted() {
    axios
      .get("https://restcountries.com/v3.1/all")
      .then((response) => {
        this.flags = response.data;
        console.log(this.flags);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
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
  /* opacity: 0.9; */
}
.menu {
  height: 300px;
  width: 100%;
  position: absolute;
  top: 80px;
  left: 120px;
  opacity: 0.7;
  border-radius: 20px;
}
.game_menu {
  font-family: poppins;
  font-size: 45px;
  color: rgb(255, 255, 255);
  background-color: black;
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
