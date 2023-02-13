<template>
  <td>
    <span v-if="isLetterVisible">
       {{randomLetter?.name}}
    </span>
    <the-preloader v-else></the-preloader>
  </td>
</template>

<script>
import ThePreloader from "./ThePreloader.vue";
import letters from "./letters";

export default {
  name: "TableBlock.vue",
  components: {ThePreloader},
  data() {
    return {
      letters,
      randomLetter: null,
      isLetterVisible: false
    }
  },
  methods: {
    getRandomLetter() {
      let random = Math.random()
      let randomLetter = this.letters[Math.floor(random * this.letters.length)]
      return randomLetter
    },
    hideLetter() {
      this.isLetterVisible = false
    },
    showLetter() {
      this.isLetterVisible = true
    },
    showLetterWithDelay(delay) {
      return new Promise(resolve => {
        setTimeout(() => {
          this.showLetter()
          resolve()
        }, delay)
      })
    },
    reRoll() {
      this.hideLetter()
      this.randomLetter = this.getRandomLetter()
      this.setNewLetter(this.randomLetter)
    },
    setNewLetter(letter) {
      this.$emit('setNewLetter', letter)
    }
  },
}
</script>

<style scoped>
 td {
   font-size: 8rem;
   border: 1px solid white;
   width: 200px;
   height: 200px;
   display: flex;
   justify-content: center;
   align-items: center;
   margin-right: 1rem;
 }
</style>