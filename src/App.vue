<template>
  <div id="app">
    <div id="player1">
      <Card
        :style="{ background: player1Color }"
        :player="1"
        :tScore="player1.overAllScore"
        :ctScore="player1.currentScore"
      />
    </div>
    <div class="btn">
      <div class="new-game-btn">
        <Button @btn-click="newGame" text="New game" pic="🔄" />
      </div>
      <div class="dice" v-if="showDice"><img :src="url" alt="dice" /></div>
      <div class="roll-btn">
        <Button @btn-click="rollDice" text="Roll a dice" pic="🎲" />
      </div>
      <div class="hold-btn">
        <Button @btn-click="holdBtn" text="Hold" pic="📥" />
      </div>
    </div>
    <div id="player2">
      <Card
        :player="2"
        :style="{ background: player2Color }"
        :tScore="player2.overAllScore"
        :ctScore="player2.currentScore"
      />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    Card,
    Button,
  },
  data() {
    return {
      player1: {
        overAllScore: 0,
        currentScore: 0,
        accumulatedCScores: [],
        accumulatedTScores: [],
        backgroundColor: "",
      },
      player2: {
        overAllScore: 0,
        currentScore: 0,
        accumulatedCScores: [],
        accumulatedTScores: [],
        backgroundColor: "",
      },
      showDice: false,
      url: "",
      player1Color: "#f8ffae",
      player2Color: "#43c6ac",
      hold: false,
      activePlayer: "player1",
    };
  },

  methods: {
    //new game
    newGame() {
      this.player1.overAllScore = 0;
      this.player1.currentScore = 0;
      this.player2.overAllScore = 0;
      this.player2.currentScore = 0;
      this.showDice = false;
      this.player1Color = "#f8ffae";
      this.player2Color = "#43c6ac";
    },

    //roll a dice
    rollDice() {
      this.showDice = true;

      let randomNum = Math.trunc(Math.random() * 6 + 1);
      this[this.activePlayer].accumulatedCScores.push(randomNum);
      const reducedCValue = this[this.activePlayer].accumulatedCScores.reduce(
        (acc, num) => {
          return acc + num;
        },
        0
      );

      this[this.activePlayer].currentScore = reducedCValue;

      if (randomNum == 1) {
        this.url = "/img/dice-1.png";
        this[this.activePlayer].accumulatedCScores = [];
        this[this.activePlayer].currentScore = 0;
        this[this.activePlayer].accumulatedTScores = [];
        this[this.activePlayer].overAllScore = 0;

        //switch player
        if (this.activePlayer == "player1") {
          this.activePlayer = "player2";
          this.player1Color = "gray";
          this.player2Color = "#43c6ac";
        } else {
          this.activePlayer = "player1";
          this.player1Color = "#f8ffae";
          this.player2Color = "gray";
        }
      }
      if (randomNum == 2) {
        this.url = "/img/dice-2.png";
      }
      if (randomNum == 3) {
        this.url = "/img/dice-3.png";
      }
      if (randomNum == 4) {
        this.url = "/img/dice-4.png";
      }
      if (randomNum == 5) {
        this.url = "/img/dice-5.png";
      }
      if (randomNum == 6) {
        this.url = "/img/dice-6.png";
      }
    },

    // hold button
    holdBtn() {
      this.hold = true;

      this[this.activePlayer].accumulatedTScores.push(
        this[this.activePlayer].currentScore
      );
      const reducedTScores = this[this.activePlayer].accumulatedTScores.reduce(
        (acc, num) => {
          return acc + num;
        },
        0
      );
      this[this.activePlayer].overAllScore = reducedTScores;
      this[this.activePlayer].accumulatedCScores = [];
      this[this.activePlayer].currentScore = 0;

      //switch players
      if (this.activePlayer == "player1") {
        this.activePlayer = "player2";
        this.player1Color = "gray";
        this.player2Color = "#43c6ac";
      } else {
        this.activePlayer = "player1";
        this.player1Color = "#f8ffae";
        this.player2Color = "gray";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #43c6ac; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to left,
    #f8ffae,
    #43c6ac
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to left,
    #f8ffae,
    #43c6ac
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

#player1 {
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

#player2 {
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

.new-game-btn {
  display: flex;
  align-items: center;
}

.btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  z-index: 3;
}

.roll-btn {
  margin-top: 170px;
  margin-bottom: 20px;
}
.dice {
  margin-top: 30px;
}
img {
  width: 100px;
  height: 100px;
}
</style>
