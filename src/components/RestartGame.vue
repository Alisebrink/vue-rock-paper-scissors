<template><button v-on:click="restartGame()">Reset game</button></template>

<script>
export default {
    data() {
        return {
            player_choice: 0,
            opponent_choice: 0
        };
    },

    methods: {
        restartGame() {
            this.player_choice = 0;
            this.opponent_choice = 0;
        }
    }
};</script>
