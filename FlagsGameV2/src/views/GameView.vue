<template>
  <div class="container_game">
    <div class="table_board">
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
      <div class="container_div" ref="container_Gaming">
        <div class="container_flagAndCounter">
          <div class="nbr_of_shot">
            <h3 class="counter_title">Coups</h3>
            <h3 class="counter">{{ gamePart }}/10</h3>
          </div>
          <img :src="countryFlag" alt="Image des drapeaux" class="countryFlag" ref="flag" />
          <div class="points">
            <h3 class="counter_title">Points</h3>
            <h3 class="counter" ref="Counter">{{ counter }}/10</h3>
          </div>
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
        <div @click="restartGame" class="next" ref="nextButton">
          <i class="fa-solid fa-arrow-right fa-2xl arrow"></i>
        </div>
        <button @click="reload" class="new_game" ref="reloadButton">Rejouer</button>
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

    // randomNameOne() {
    //   this.flag.map(() => {
    //     const randomIndex = Math.floor(Math.random() * this.flag.length)
    //     const randomElement = this.flag[randomIndex]
    //     this.dataNameRandomOne = randomElement.translations.fra.common
    //     console.log(randomElement)
    //   })
    // },
    // randomNameTwo() {
    //   this.flag.map(() => {
    //     const randomIndex = Math.floor(Math.random() * this.flag.length)
    //     const randomElement = this.flag[randomIndex]
    //     this.dataNameRandomTwo = randomElement.translations.fra.common
    //   })
    // },

    randomNameOne() {
      const randomIndex = Math.floor(Math.random() * this.flag.length)
      const randomElement = this.flag[randomIndex]
      this.dataNameRandomOne = randomElement.translations.fra.common
    },
    randomNameTwo() {
      do {
        const randomIndex = Math.floor(Math.random() * this.flag.length)
        const randomElement = this.flag[randomIndex]
        this.dataNameRandomTwo = randomElement.translations.fra.common
      } while (this.dataNameRandomOne === this.dataNameRandomTwo)
    },

    //  comportement des classes (chgmt couleur) suite à la réponse du User.................................

    reponse(event) {
      this.$refs.divGreen.classList.add('correct')
      this.$refs.divRedOne.classList.add('incorrect')
      this.$refs.divRedTwo.classList.add('incorrect')
      this.$refs.divGreen.classList.add('disabled')
      this.$refs.divRedOne.classList.add('disabled')
      this.$refs.divRedTwo.classList.add('disabled')
      if (event.target.textContent == this.countryName) this.counter++

      //incrémenter à chaque clique des trois divs questions pour déterminer le nombre de coups par partie.......................................

      this.gamePart++
      if (this.gamePart === 10) {
        this.$nextTick(() => {
          this.$refs.reloadButton.scrollIntoView({
            behavior: 'smooth',
            block: 'end',
            inline: 'nearest'
          })
        })
        this.$refs.Counter.classList.add('counter_black')
        this.$refs.reloadButton.classList.add('new_game_visible')
        this.$refs.divGreen.classList.add('disabled')
        this.$refs.divRedOne.classList.add('disabled')
        this.$refs.divRedTwo.classList.add('disabled')
        this.$refs.nextButton.classList.add('disabled')
        this.$refs.containerCounter.classList.add('container_counter_resultat')
      }
    },
    restartGame() {
      // réinitialisation du jeu ici
      this.$refs.divGreen.classList.remove('correct')
      this.$refs.divRedOne.classList.remove('incorrect')
      this.$refs.divRedTwo.classList.remove('incorrect')
      this.$refs.divGreen.classList.remove('disabled')
      this.$refs.divRedOne.classList.remove('disabled')
      this.$refs.divRedTwo.classList.remove('disabled')
      this.oneflag()
      this.randomNameOne()
      this.randomNameTwo()
      this.shuffle()
    },
    reload() {
      window.location.reload()
    },
    shuffle() {
      const parent = this.$refs.containerQuestionRandom
      const elements = parent.children
      for (let i = 0; i < elements.length; i++) {
        parent.appendChild(elements[Math.floor(Math.random() * elements.length)])
      }
    },
    findUrl(index) {
      let dataUrl = [this.urlA, this.urlB, this.urlC, this.urlD, this.urlE, this.urlF]
      this.urlSelected = dataUrl[index]
      this.fetchData()
      this.$refs.flag.classList.add('countryFlag_visible')
      this.$refs.container_Gaming.classList.add('container_div_visible')
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
          this.showNewGameButton = true
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
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
}
.container_Gaming {
  height: 100vh;
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: -30px;
}
.container_flagAndCounter {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 60px;
}
.container_counter {
  height: 550px;
  margin-top: 78px;
  width: 200px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-around;
  border: solid white 1px;
  box-shadow: 1px 1px 3px black;
}
.container_countries_names {
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  align-content: center;
  justify-content: center;
  width: 80%;
  height: 30%;
}
.countries_names {
  color: rgb(1, 1, 72);
  box-shadow: 1px 1px 7px 0px rgb(83, 82, 82);
  background-color: white;
  width: 100%;
  padding: 10px;
  font-size: 17px;
  border-radius: 15px;
  transition: 0.4s ease-in-out;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container_div {
  visibility: hidden;
}
.container_div_visible {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 600px;
  visibility: visible;
  width: 100%;
  gap: 20px;
}

.counter {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  color: rgb(255, 255, 255);
  border: solid 1px white;
  padding: 10px;
  border-radius: 10px;
  background-color: transparent;
  width: 100px;
  height: 100px;
  padding: 20px;
  box-shadow: 1px 1px 5px rgb(30, 30, 30);
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
  visibility: hidden;
}
.countryFlag_visible {
  height: 220px;
  width: 330px;
  box-shadow: 1px 1px 6px 0px rgb(69, 64, 64);
  border-radius: 2px;
  border: solid white 3px;
  /* margin-bottom: 20px;
  margin-top: 20px; */
  visibility: visible;
}
.input {
  border: none;
  box-shadow: 1px 1px 4px 0px rgb(69, 64, 64) inset;
  width: auto;
}

.correct {
  background: linear-gradient(rgb(152, 253, 0), rgb(18, 200, 5));
  box-shadow: 1px 1px 3px rgb(39, 38, 38) inset, -1px 1px 3px rgb(39, 38, 38) inset;
  color: rgb(255, 255, 255);
}
.incorrect {
  background: linear-gradient(rgb(236, 43, 43), rgb(231, 36, 36));
  color: white;
  box-shadow: 1px 1px 3px rgb(39, 38, 38) inset, -1px 1px 3px rgb(39, 38, 38) inset;
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
  margin-top: 10px;
  visibility: visible;
  background-color: rgb(38, 38, 80);
  color: rgb(255, 255, 255);
  border-radius: 10px;
  box-shadow: 1px 1px 4px 0px rgb(4, 4, 4);
  height: 80px;
  width: 120px;
  border: none;
  font-size: 18px;
  padding: 20px;
  border: solid white 2px;
  transform: scale();
  transition: 0.2s ease-in;
}
.new_game_visible:hover {
  box-shadow: 3px 3px 3px black inset;
  transform: scale(0.9);
}
.table_board {
  background-color: white;
  box-shadow: 2px -1px 5px black inset;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  padding-top: 30px;
  padding-bottom: 40px;
  border-radius: 7px;
  width: 100%;
  z-index: 1;
}
.table_board h1 {
  color: white;
  font-size: 14px;
  text-transform: uppercase;
  font-weight: bold;
}
.themes {
  margin-top: 10px;
  height: 20px;
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-left: 220px;
  margin-right: 220px;
}
.continent {
  color: orangered;
  font-size: 13px;
  height: 50px;
  width: 100px;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
  align-content: center;
  font-family: poppins;
  letter-spacing: 0px;
  text-transform: uppercase;
  font-weight: 700;
  gap: 5px;
}
.next {
  background-color: #600dff;
  width: 60px;
  height: 60px;
  font-size: 14px;
  border-radius: 50%;
  border: 1px solid rgb(53, 50, 50);
  transition: 0.4s ease-in-out;
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;
  box-shadow: 1px 1px 5px rgb(23, 23, 23);
  transition: 0.1s ease-in-out;
}
.next2 {
  color: rgb(217, 16, 16);
  width: 60px;
  height: 60px;
  font-size: 14px;
  border-radius: 50%;
  border: 1px solid rgb(53, 50, 50);
  transition: 0.4s ease-in-out;
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;
  box-shadow: 1px 1px 5px rgb(23, 23, 23);
  transition: 0.1s ease-in-out;
}
.arrow {
  color: white;
}
.counter_black {
  background-color: black;
}

/* ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ */

@media screen and (max-width: 768px) {
  .container_game {
    margin-top: 10px;
  }
  .countries_names {
    font-size: 14px;
  }
  .countryFlag_visible {
    height: 100px;
    width: 100px;
    box-shadow: 1px 1px 6px 0px rgb(69, 64, 64);
    border-radius: 2px;
    border: solid white 3px;
    /* margin-bottom: 20px;
  margin-top: 20px; */
    visibility: visible;
  }
  .counter {
    display: flex;
    align-items: left;
    justify-content: center;
    font-size: 14px;
    color: rgb(255, 255, 255);
    border: solid 1px white;
    border-radius: 10px;
    background-color: transparent;
    width: 70px;
    height: 70px;
    padding: 20px;
    box-shadow: 1px 1px 5px rgb(30, 30, 30);
  }
  .container_flagAndCounter {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    gap: 15px;
  }
  .countryFlag_visible {
    height: 110px;
    width: 150px;
    box-shadow: 1px 1px 6px 0px rgb(69, 64, 64);
    border-radius: 2px;
    border: solid white 3px;
    visibility: visible;
  }
  .table_board {
    background-color: white;
    box-shadow: 1px -1px 3px black inset, -1px 1px 3px black inset;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 20px;
    padding-bottom: 40px;
    border-radius: 7px;
    width: 90%;
    height: 30px;
    z-index: 1;
    margin-top: 10px;
  }
  .continent {
    color: orangered;
    font-size: 10px;
    height: 30px;
    width: 100px;
    display: flex;
    flex-direction: column;
    align-items: center;
    align-content: center;
    font-family: poppins;
    letter-spacing: 0px;
    text-transform: uppercase;
    font-weight: 700;
    gap: -5px;
    margin-top: 0px;
  }
  .container_div_visible {
    margin-top: 70px;
    display: flex;
    flex-direction: column;
    align-items: center;
    visibility: visible;
    width: 100%;
    gap: 20px;
  }
}

/* +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ */

@media screen and (min-width: 768px) {
  .container_countries_names {
    width: 400px;
  }
  .next {
    background-color: #600dff;
    width: 60px;
    height: 60px;
    font-size: 14px;
    border-radius: 30%;
    border: 1px solid rgb(53, 50, 50);
    transition: 0.4s ease-in-out;
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
    box-shadow: 1px 1px 5px rgb(23, 23, 23);
    transition: 0.1s ease-in-out;
  }
  .table_board {
    margin-top: 5px;
    box-shadow: 2px -1px 5px black inset, -2px 1px 5px black inset;
    width: 90%;
  }
}
</style>
