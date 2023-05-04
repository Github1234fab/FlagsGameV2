<template>
  <div class="header">
    <div class="logo_container">
      <h1 class="title_header">FlagsGame</h1>
     <!-- <i class="fa-solid fa-flag fa-lg logo"></i> -->
    </div>
    <nav>
      <router-link to="/" class="game_menu"> Home</router-link>
      <router-link to="/game" class="game_menu"> Drapeaux</router-link>
      <h2 class="game_menu">Capitales</h2>
      <h2 class="game_menu">Habitants</h2>
      <h2 class="game_menu">Monnaies</h2>
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
  background: linear-gradient(to bottom, #2e2e2e 80%, transparent);
  display: flex;
  flex-direction: column;
  /* justify-content: space-around; */
  align-items: center;
  align-content: center;
}
.title_header {
  color: white;
  font-size: 29px;
  margin-top: 15px;
  -webkit-background-clip: text;
  background-image: linear-gradient(to left, orange 23% , rgb(86, 86, 242), pink );
  color: transparent;

}
nav {
  width: 90%;
  display: flex;
  justify-content: space-around; 
}

.game_menu {
  margin-top: 20px;
  font-family: poppins;
  font-size: 14px;
  color: rgb(255, 255, 255);
  transition: .200s ease-in-out;
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
