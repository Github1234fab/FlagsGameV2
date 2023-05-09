<template>
  <div class="header">
    <div class="logo_container">
      <h1 class="title_header">FlagsGame</h1>
      <!-- <i class="fa-solid fa-flag fa-lg logo"></i> -->
    </div>
    <nav>
      <router-link to="/" class="game_menu"> Home</router-link>
      <router-link to="/game" class="game_menu"> Drapeaux</router-link>
      <router-link to="" class="game_menu">Capitales</router-link>
      <router-link to="" class="game_menu">Habitants</router-link>
      <router-link to="" class="game_menu">Monnaies</router-link>
    </nav>
  </div>
</template>
<script></script>
<style>
body {
  background-color: black;
}
.header {
  height: 120px;
  width: 100%;
  background-color: #2e2e2e;
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.title_header {
  color: white;
  font-size: 29px;
  margin-top: 15px;
  -webkit-background-clip: text;
  background-image: linear-gradient(to left, orange 23%, rgb(86, 86, 242), pink);
  color: transparent;
}
nav {
  width: 100%;
  display: flex;
  justify-content: space-around;
}
.game_menu {
  margin-top: 20px;
  font-family: poppins;
  font-size: 14px;
  color: rgb(255, 255, 255);
  transition: 0.2s ease-in-out;
  transform: scale() rotate();
  /* text-shadow: 0px 0px 1px #ffffff;  */
}
.game_menu:hover {
  transform: scale(1.1) rotate(4deg);
}
.logo {
  margin-top: 10px;
  color: white;
  transform: rotate(0deg);
  transition: 0.2s ease-in-out;
  transform: scale(1);
}
.logo:hover {
  color: rgb(236, 243, 236);
  transform: scale(1.2);
  transform: rotate(5deg);
}
.logo_container {
  display: flex;
  justify-content: space-around;
  width: 180px;
  align-items: center;
}

@media screen and (max-width: 768px) {
  .header {
    height: 120px;
    width: 100%;
    background-color: #2e2e2e;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
  }
  nav {
    width: 100%;
    display: flex;
  }
  .game_menu {
    margin-top: 0px;
    font-family: poppins;
    font-size: 12px;
    color: rgb(255, 255, 255);
    transition: 0.2s ease-in-out;
    transform: scale() rotate();
    margin-top: -20px;
  }
}
</style>
