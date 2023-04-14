<template>
  <div class="container_homePage">
    <div class="container_menu">
         <router-link to="/game" class="game_menu">Quel est le nom du pays?</router-link>
      <h2 class="game_menu">Quelle est sa capitale?</h2>
      <h2 class="game_menu">Comment s'appellent ses habitants?</h2>
      <h2 class="game_menu">Quelle est le nom de sa monnaie?</h2>
    </div>
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

.game_menu {
  width: 200px;
  font-family: poppins;
  font-size: 18px;
  color: rgb(255, 255, 255);
  text-shadow: 0px 0px 10px #ffffff; 
}

a{
  text-decoration: none;
}

.container_homePage {
  display: flex;
  height: 100vh;
  width: 100%;
  background: url('../assets/DALL·E 2023-04-06 15.15.01 - a design of mountains on which are planted all the flags of the world with blue sky.png');
  background-size: cover;
}

.container_menu {
  width: 100%;
  display: flex;
  justify-content: space-around;
  height: 300px;
  margin-top: 50px;

}

</style>
