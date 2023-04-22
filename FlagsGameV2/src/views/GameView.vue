<template>
  <div class="container_game">
    <div class="table_board">
      <h1>Choisis un continent</h1>
      <div class="themes">
        <span class="continent"
          >Europe <input @click="findUrl(0)" type="radio" name="continent"
        /></span>
        <span class="continent"
          >Asie <input @click="findUrl(1)" type="radio" name="continent"
        /></span>
        <span class="continent"
          >Amérique<input @click="findUrl(2)" type="radio" name="continent"
        /></span>
        <span class="continent"
          >Afrique <input @click="findUrl(3)" type="radio" name="continent"
        /></span>
        <span class="continent"
          >Océanie <input @click="findUrl(4)" type="radio" name="continent"
        /></span>
        <span class="continent"
          >Monde<input @click="findUrl(5)" type="radio" name="continent"
        /></span>
      </div>
    </div>
    <div class="container_Gaming">
      <div class="container_gamer" ref="containerGamer">
        <div class="container_counter" ref="containerCounter">
          <h3 class="counter_title">Points</h3>
          <h3 class="counter">{{ counter }}</h3>
          <h3 class="counter_title">Coups</h3>
          <h3 class="counter">{{ gamePart }} /10</h3>
          <!-- <p class="resultat" ref="resultat">{{ counter }} points sur 10.</p> -->
          <button ref="newGame" @click="reload" class="new_game">Rejouer ?</button>
        </div>

        <div class="container_div">
          <img :src="countryFlag" alt="Image des drapeaux" class="countryFlag" ref="flag" />
          <h3 class="question">À quel pays appartient ce drapeau?</h3>
          <div ref="suivant" @click="restartGame" class="next">
            <i class="fa-solid fa-arrow-right fa-2xl arrow"></i>
          </div>
          <div class="container_countries_names" ref="containerQuestionRandom">
            <div @click="reponse" class="countries_names" ref="divRedOne">
              {{ dataNameRandomOne }}
            </div>
            <div @click="reponse" class="countries_names" ref="divRedTwo">
              {{ dataNameRandomTwo }}
            </div>
            <div @click="reponse" class="countries_names" ref="divGreen">{{ countryName }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      urlA: 'https://restcountries.com/v3.1/region/europe',
      urlB: 'https://restcountries.com/v3.1/region/asia',
      urlC: 'https://restcountries.com/v3.1/region/america',
      urlD: 'https://restcountries.com/v3.1/region/africa',
      urlE: 'https://restcountries.com/v3.1/region/Oceania',
      urlF: 'https://restcountries.com/v3.1/all',
      flag: [],
      countryName: '',
      countryFlag: '',
      dataReponse: '',
      dataNameRandomOne: '',
      dataNameRandomTwo: '',
      isCorrect: false,
      userClicked: false,
      counter: 0,
      gamePart: 0,
      disabledDivs: false,
      urlSelected: ''
    }
  },
  methods: {
    //  récupération des datas.name et data.flag
    oneflag() {
      this.flag.map(() => {
        const randomIndex = Math.floor(Math.random() * this.flag.length)
        const randomElement = this.flag[randomIndex]
        this.countryName = randomElement.translations.fra.common
        this.countryFlag = randomElement.flags.png
        console.log(this.countryName)
        console.log(this.countryFlag)
      })
    },
    //fonction pour obtenir deux noms aléatoires qui seront associés au vrai nom de drapeau...................

    randomNameOne() {
      this.flag.map(() => {
        const randomIndex = Math.floor(Math.random() * this.flag.length)
        const randomElement = this.flag[randomIndex]
        // const randomElements = this.flag.sort(() => 0.5 - Math.random()).slice(0, 1)
        this.dataNameRandomOne = randomElement.translations.fra.common
        console.log(this.dataNameRandomOne)
      })
    },
    randomNameTwo() {
      this.flag.map(() => {
        const randomIndex = Math.floor(Math.random() * this.flag.length)
        const randomElement = this.flag[randomIndex]
        // const randomElements = this.flag.sort(() => 0.5 - Math.random()).slice(0, 1)
        this.dataNameRandomTwo = randomElement.translations.fra.common
        console.log(this.dataNameRandomTwo)
      })
    },
    //  comportement des classes (chgmt couleur) suite à la réponse du User.................................

    reponse(event) {
      this.$refs.divGreen.classList.add('correct')
      this.$refs.divRedOne.classList.add('incorrect')
      this.$refs.divRedTwo.classList.add('incorrect')
      if (event.target.textContent == this.countryName) this.counter++

      //incrémenter à chaque clique des trois divs questions pour déterminer le nombre de coups par partie.......................................

      console.log('ok')
      this.gamePart++
      console.log(this.gamePart)
      if (this.gamePart == 10) {
        console.log('Tu as fait une partie en 10')
        this.$refs.divGreen.classList.add('disabled')
        this.$refs.divRedOne.classList.add('disabled')
        this.$refs.divRedTwo.classList.add('disabled')
        // this.$refs.resultat.classList.add('resultat_visible')
        this.$refs.newGame.classList.add('new_game_visible')
        this.$refs.containerCounter.classList.add('container_counter_resultat')
        this.$refs.suivant.classList.add('disabled')
      }
    },
    restartGame() {
      // réinitialisation du jeu ici
      this.$refs.divGreen.classList.remove('correct')
      this.$refs.divRedOne.classList.remove('incorrect')
      this.$refs.divRedTwo.classList.remove('incorrect')
      this.oneflag()
      this.randomNameOne()
      this.randomNameTwo()
      this.shuffle()
    },
    reload() {
      // this.oneflag()
      // this.randomNameOne()
      // this.randomNameTwo()
      // this.shuffle()
      // this.counter = 0
      // this.$refs.divGreen.classList.remove('correct')
      // this.$refs.divRedOne.classList.remove('incorrect')
      // this.$refs.divRedTwo.classList.remove('incorrect')
      // this.$refs.divGreen.classList.remove('disabled')
      // this.$refs.divRedOne.classList.remove('disabled')
      // this.$refs.divRedTwo.classList.remove('disabled')
      // this.$refs.suivant.classList.remove('disabled')
      // // this.$refs.resultat.classList.remove('resultat_visible')
      // this.$refs.newGame.classList.remove('new_game_visible')
      // this.$refs.containerCounter.classList.remove('container_counter_resultat')
      window.location.reload()
    },
    shuffle() {
      const parent = this.$refs.containerQuestionRandom
      const elements = parent.children
      for (let i = 0; i < elements.length; i++) {
        parent.appendChild(elements[Math.floor(Math.random() * i)])
      }
    },
    findUrl(index) {
      let dataUrl = [this.urlA, this.urlB, this.urlC, this.urlD, this.urlE, this.urlF]
      this.urlSelected = dataUrl[index]
      console.log(this.urlSelected)
      this.fetchData()
      this.$refs.flag.classList.add('countryFlag_visible')
      console.log('ok')
      this.$refs.containerGamer.classList.add('container_gamer_visible')
    },
    fetchData() {
      axios
        .get(this.urlSelected)
        .then((response) => {
          this.flag = response.data
          console.log(this.flag)
          this.oneflag()
          this.randomNameOne()
          this.randomNameTwo()
          this.quizz()
          this.shuffle()
          this.gamePart()
          this.reload()
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
.container_game {
  /* background: radial-gradient(circle, blue, white); */
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 5px;
}
.container_counter {
  height: 250px;
  width: 100px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  position: absolute;
  left: 560px;
  top: 20px;
}

.container_countries_names {
  margin-top: 40px;
  display: flex;
  height: 50px;
  gap: 10px;
  align-items: center;
  align-content: center;
  justify-content: center;
  width: 600px;
}
.container_gamer {
  visibility: hidden;
}
.container_gamer_visible {
  visibility: visible;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  background-color: white;
  align-items: center;
  align-content: center;
  border-radius: 15px;
  height: 500px;
  width: 700px;
  position: relative;
  border: solid rgb(137, 165, 237) 10px;
  box-shadow: 1px 1px 5px grey;
}

.container_div {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.counter {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  color: rgb(53, 51, 51);
  /* border: solid 1px rgb(110, 106, 106); */
  padding: 10px;
  border-radius: 10px;
  background-color: transparent;
  width: 100px;
  height: 50px;
  padding: 20px;
  box-shadow: 1px 1px 5px grey;
}
.counter_title {
  color: rgb(51, 51, 49);
  font-size: 16px;
  text-align: center;
  font-weight: 400;
  font-family: poppins;
}

.question {
  font-size: 18px;
  color: rgb(1, 21, 42);
  margin-top: 20px;
  text-transform: uppercase;
  font-weight: bold;
}
.game_starter {
  height: 70px;
  width: 70px;
  background-color: rgb(24, 237, 24);
  color: white;
  border: none;
  box-shadow: 1px 1px 6px 0px rgb(69, 64, 64) inset;
}
.countryFlag {
  /* height: 200px;
  width: 240px; */
  box-shadow: 1px 1px 6px 0px rgb(69, 64, 64);
  border-radius: 2px;
  margin-bottom: 20px;
  margin-top: 20px;
  visibility: hidden;
}
.countryFlag_visible {
  height: 220px;
  width: 320px;
  box-shadow: 1px 1px 6px 0px rgb(69, 64, 64);
  border-radius: 2px;
  margin-bottom: 20px;
  margin-top: 20px;
  visibility: visible;
}
.input {
  border: none;
  box-shadow: 1px 1px 4px 0px rgb(69, 64, 64) inset;
  width: auto;
}
.countries_names {
  color: rgb(1, 1, 72);
  box-shadow: 1px 1px 7px 0px rgb(83, 82, 82);
  background-color: white;
  width: 350px;
  padding: 10px;
  font-size: 17px;
  border-radius: 15px;
  transition: 0.4s ease-in-out;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.correct {
  background: linear-gradient(rgb(152, 253, 0), rgb(18, 200, 5));
  box-shadow: 1px 1px 3px rgb(39, 38, 38);
  color: rgb(255, 255, 255);
}
.incorrect {
  background: linear-gradient(rgb(236, 43, 43), rgb(231, 36, 36));
  color: white;
  box-shadow: 1px 1px 3px rgb(39, 38, 38);
}
.clicked-wrong {
  background: linear-gradient(rgb(242, 43, 43), rgb(229, 115, 115));
  color: rgb(255, 255, 255);
}

.disabled {
  pointer-events: none;
}
.abled {
  pointer-events: all;
}
/* .resultat {
  visibility: hidden;
} */
/* .new_game {
  visibility: hidden;
} */
.resultat {
  visibility: visible;
  color: white;
  margin-top: 10px;
  transition: visibility2s ease-in;
}
.new_game {
  visibility: hidden;
}
.new_game_visible {
  visibility: visible;
  background-color: rgb(38, 38, 80);
  color: rgb(255, 255, 255);
  border-radius: 10px;
  box-shadow: 1px 1px 4px 0px rgb(4, 4, 4);
  height: 60px;
  border: none;
  transition: visibility 2s ease-in;
  font-size: 18px;
}
.table_board {
  background: linear-gradient(to top, transparent, rgb(11, 91, 141), transparent);
  /* background: linear-gradient(to left, rgb(178, 180, 29), 10%, rgb(190, 190, 70)); */
  display: flex;
  flex-direction: column;
  align-content: center;
  align-items: center;
  justify-content: space-around;
  width: 100%;
  padding: 20px;
  /* border-radius: 15px; */
  /* box-shadow: 1px 1px 5px grey; */
}
.table_board h1 {
  color: white;
  font-size: 18px;
  text-transform: uppercase;
  font-weight: bold;
}
.themes {
  margin-top: 10px;
  height: 200px;
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-left: 220px;
  margin-right: 220px;
}
.continent {
  color: white;
  height: 50px;
  width: 100px;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.next {
  color: rgb(117, 217, 16);
  width: 50px;
  height: 50px;
  padding: 10px;
  margin-bottom: 5px;
  font-size: 14px;
  border-radius: 50%;
  border: 1px solid rgb(53, 50, 50);
  transition: 0.4s ease-in-out;
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;
  gap: 10px;
  margin-top: 10px;
  position: absolute;
  top: 290px;
  left: 590px;
  box-shadow: 1px 1px 5px grey;
}
.arrow {
  color: rgb(117, 217, 16);
}
</style>
