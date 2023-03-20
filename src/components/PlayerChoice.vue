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
  },
};
</script>

<style>
.choices {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
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
}

}
</style>
