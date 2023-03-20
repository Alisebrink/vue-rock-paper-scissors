<template>
  <section class="mainContainer">
    <header class="header"><h1>Lets play rock, paper, scissor!</h1></header>

    <div class="gameContainer">
      <div>
        <p>
          Welcome to play the game rock, paper, scissor! Make your selection and
          start the game!
        </p>
      </div>

      <div class="playerChoice">
        <Player
          v-on:getChoice="updatePlayerChoice($event)"
          v-bind:choice="player_choice"
        />
        <div>
          <p class="playerChose">
            You chose: <span>{{ player_choice }}</span>
          </p>
          <p class="opponentChose">
            Your opponent chose: <span>{{ opponent_choice }}</span>
          </p>
        </div>

        <p class="whoWon" v-if="winner">{{ winner }}</p>
      </div>
      <div class="scoreboard">
        <h2>Scoreboard</h2>
        <div class="score">
          <p>
            You: <span>{{ player_score }}</span>
          </p>
          <p>
            Opponent: <span>{{ opponent_score }}</span>
          </p>
        </div>
      </div>
      <div class="buttons">
        <Opponent
          @click="play"
          v-on:getChoice="updateOpponentScore($event)"
          v-bind:choice="opponent_choice"
        />
        <RestartGame @click="restart" />
      </div>
    </div>
  </section>
</template>

<script>
import Player from "./components/PlayerChoice.vue";
import Opponent from "./components/OpponentChoice.vue";
import RestartGame from "./components/RestartGame.vue";

export default {
  name: "App",
  el: "#choices",
  components: {
    Player,
    Opponent,
    RestartGame,
  },
  data() {
    return {
      player_choice: "",
      opponent_choice: "",
      player_score: 0,
      opponent_score: 0,
      winner: "Start playing to see who won!",
    };
  },
  methods: {
    updatePlayerChoice(choice) {
      this.player_choice = choice;
    },
    updateOpponentScore(choice) {
      this.opponent_choice = choice;
    },
    ImgScr() {
      if (this.opponent_choice == "Rock") {
        return "sten.png";
      } else if (this.opponent_choice == "Paper") {
        return "påse.png";
      } else {
        return "sax.png";
      }
    },
    play() {
      const { player_choice, opponent_choice } = this;

      if (player_choice === opponent_choice) {
        this.winner = "It's a tie!";
      } else if (
        (opponent_choice === "Scissor" && player_choice === "Paper") ||
        (opponent_choice === "Rock" && player_choice === "Scissor") ||
        (opponent_choice === "Paper" && player_choice === "Rock")
      ) {
        this.opponent_score++;
        this.winner = "Your opponent won! :(";
      } else if (player_choice === "") {
        alert("You have to make a choice!");
        this.opponent_choice = "";
      } else {
        this.player_score++;
        this.winner = "You won, congratulations!";
      }
    },
    restart() {
      this.player_choice = "";
      this.opponent_choice = "";
      this.player_score = "";
      this.opponent_score = "";
      this.winner = "Start playing to see who won!";
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Merriweather:wght@400;700&family=Montserrat:wght@400;700&display=swap");

body {
  background-image: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
  font-family: "Montserrat", sans-serif;
  font-size: 1.2em;
  padding: 0px;
  margin: 0px;
  color: black;
  background-repeat: no-repeat;
  background-attachment: fixed;
}

h1 {
  padding: 0;
  margin: 0;
}

.mainContainer {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  background: white;
}

.header {
  background: #242424;
  color: white;
  font-weight: 700;
  padding: 10px;
  text-align: center;
  font-size: 12px;
  border-radius: 5px 5px 0px 0px;
}

.gameContainer {
  padding: 20px;
  position: relative;
  text-align: center;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 20vh 35vh 20vh 10vh;
}

.gameContainer div + p {
  grid-column: 1 / span 1;
  grid-row: 1 / span 1;
}
.playerChoice {
  grid-column: 1 / span 1;
  grid-row: 2 / span 1;
}
.scoreboard {
  grid-column: 1 / span 1;
  grid-row: 3 / span 1;
}
.buttons {
  grid-column: 1 / span 1;
  grid-row: 4 / span 1;
}

.playerChoice div:nth-child(1) {
  margin-bottom: 10px;
}

.playerChoice div:nth-child(2) {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.playerChose,
.opponentChose {
  color: #667eea;
  font-weight: 700;
  margin: 5px;
}

.playerChose span,
.opponentChose span {
  color: black;
  font-weight: 300;
}

.scoreboard {
  width: 100%;
  text-align: left;
}

.scoreboard h2 {
  color: #667eea;
  border-bottom: 2px solid #667eea;
  font-size: 1.2rem;
}

.playerChoice {
  color: black;
}

.score p span {
  color: #667eea;
  font-weight: 700;
}

.buttons {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 100%;
  height: 40px;
  gap: 20px;
  align-self: flex-end;
  margin-top: auto;
}

.buttons button {
  font-size: 1rem;
  border: none;
  border-radius: 3px;
  background: #242424;
  color: white;
  font-weight: 700;
  flex: auto;
}

.buttons button:nth-child(2) {
  background: #cccccc;
}

.buttons button:hover {
  cursor: pointer;
  background: #764ba2;
  transition: 0.1s;
}

@media only screen and (min-width: 599px) {
  body {
    padding: 50px;
  }

  .mainContainer {
    width: calc(100% - 40px);
    margin: 0 auto;
    border-radius: 5px;
    box-shadow: 0px 3px 15px rgb(0, 0, 0, 0.15);
  }

  .gameContainer {
    padding: 40px;
    display: flex;
    flex-direction: column;
  }

  .playerChoice {
    margin-top: 50px;
  }

  .playerChoice div:nth-child(1) {
    margin-bottom: 30px;
  }

  .playerChoice div:nth-child(2) {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  .scoreboard {
    width: 250px;
    text-align: left;
  }

  .whoWon {
    text-align: left;
  }

  .buttons {
    display: flex;
    gap: 20px;
    position: absolute;
    bottom: 30px;
    right: 30px;
    width: auto;
  }

  .buttons button {
    padding: 10px 35px;
    font-size: 20px;
    border: none;
    font-weight: 700;
  }

  .buttons button:hover {
    cursor: pointer;
    transition: 0.1s;
  }
}
</style>
