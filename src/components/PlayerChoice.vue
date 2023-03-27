<template>
  <div id="choices" class="choices">
    <img
      type="button"
      :src="hoverOnRock"
      @mouseover="setHoverRock = true"
      @mouseleave="setHoverRock = false"
      alt="Välj sten"
      v-on:click="rockChosen()"
    />
    <img
      type="button"
      :src="hoverOnPaper"
      @mouseover="setHoverPaper = true"
      @mouseleave="setHoverPaper = false"
      alt="Välj påse"
      v-on:click="paperChosen()"
    />
    <img
      type="button"
      :src="hoverOnScissor"
      @mouseover="setHoverScissor = true"
      @mouseleave="setHoverScissor = false"
      alt="Välj sax"
      v-on:click="scissorChosen()"
    />
    <img
      type="button"
      :src="hoverOnLizard"
      @mouseover="setHoverLizard = true"
      @mouseleave="setHoverLizard = false"
      alt="Välj sax"
      v-on:click="lizardChosen()"
    />
    <img
      type="button"
      :src="hoverOnSpock"
      @mouseover="setHoverSpock = true"
      @mouseleave="setHoverSpock = false"
      alt="Välj sax"
      v-on:click="spockChosen()"
    />
  </div>
</template>

<script>
export default {
  el: "#choices",
  data() {
    return {
      rock: require("../assets/sten.png"),
      rockHover: require("../assets/sten-hover.png"),
      setHoverRock:false,
      paper: require("../assets/påse.png"),
      paperHover: require("../assets/påse-hover.png"),
      setHoverPaper:false,
      scissor: require("../assets/sax.png"),
      scissorHover: require("../assets/sax-hover.png"),
      setHoverScissor:false,
      lizard: require("../assets/lizard.png"),
      lizardHover: require("../assets/lizard-hover.png"),
      setHoverLizard:false,
      spock: require("../assets/spock.png"),
      spockHover: require("../assets/spock-hover.png"),
      setHoverSpock:false,
    }
  },

  computed: {
    hoverOnRock () {
      if (this.setHoverRock == true) {
        return this.rockHover
      } else {
        return this.rock
      }
    },
    hoverOnPaper () {
      if (this.setHoverPaper == true) {
        return this.paperHover
      } else {
        return this.paper
      }
    },
    hoverOnScissor () {
      if (this.setHoverScissor == true) {
        return this.scissorHover
      } else {
        return this.scissor
      }
    },
    hoverOnLizard () {
      if (this.setHoverLizard == true) {
        return this.lizardHover
      } else {
        return this.lizard
      }
    },
    hoverOnSpock () {
      if (this.setHoverSpock == true) {
        return this.spockHover
      } else {
        return this.spock
      }
    },
  },

  methods: {
    rockChosen() {
      this.$emit("getChoice", "Rock");
    },
    paperChosen() {
      this.$emit("getChoice", "Paper");
    },
    scissorChosen() {
      this.$emit("getChoice", "Scissor");
    },
    lizardChosen() {
      this.$emit("getChoice", "Lizard");
    },
    spockChosen() {
      this.$emit("getChoice", "Spock");
    },
  },
};
</script>

<style>
.choices {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
  margin:0 auto;
}

.choices img {
  width:25vw;
}

.choices img:hover {
  cursor: pointer;
}

@media only screen and (min-width:599px) {
  .choices {
  flex-direction: row;
  gap: 50px;
}

.choices img {
  width:auto;
  max-width:150px;
}

}
</style>
