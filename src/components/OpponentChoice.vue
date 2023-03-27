<template>
        <button v-on:click="randomChoice()">Let's play!</button>
</template>

<script>
const choices = ['Rock', 'Paper', 'Scissor', 'Lizard', 'Spock'];

export default {
    data() {
        return {
            choice: "",
        };
    },

    methods: {
        randomChoice() {
            const randomChoiceIndex = Math.floor(Math.random() * choices.length);
            this.choice = choices[randomChoiceIndex];
            this.$emit('getChoice', this.choice);
        }
    }
};


</script>