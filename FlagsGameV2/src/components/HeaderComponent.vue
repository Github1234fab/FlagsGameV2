<template>
  <div class="header">
    <div class="logo_container">
      <h1 class="title_header">FlagsGame</h1>
     <i class="fa-solid fa-flag fa-lg logo"></i>
    </div>
    <nav>
      <router-link to="/" class="game_menu"> Home</router-link>
      <router-link to="/game" class="game_menu"> Drapeau</router-link>
      <h2 class="game_menu">Capitale</h2>
      <h2 class="game_menu">Habitants</h2>
      <h2 class="game_menu">Monnaie</h2>
    </nav>
  </div>
</template>
<script></script>
<style>
body{
  background-color: black;
}

.header {
   height:150px;
  width: 100%;
  background-color: #1a4c70;
  display: flex;
  flex-direction: column;
  /* justify-content: space-around; */
  align-items: center;
  align-content: center;
  background: linear-gradient(to bottom, #1a4c70, 90%,  transparent);
}
.title_header {
  color: white;
  font-size: 22px;
  margin-top: 20px;
}
nav {
  width: 100%;
  display: flex;
  justify-content: space-around; 
}

.game_menu {
  margin-top: 20px;
  font-family: oswald;
  font-size: 18px;
  color: rgb(255, 255, 255);
  transition: .200s ease-in-out;
  /* text-shadow: 0px 0px 1px #ffffff;  */
}
.game_menu:hover {
 font-size: 20px;
}
.logo {
  margin-top: 10px;
  color: white;
  transform: rotate(0deg);
  transition: .200s ease-in-out;
   transform: scale(1);
}
.logo:hover{
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
</style>
