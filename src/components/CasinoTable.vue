<template>
  <div>
    <div class="score">SCORE: {{score}}</div>
    <table>
      <tr class="d-flex">
        <table-block ref="firstBlock" @set-new-letter="letters.first = $event"></table-block>
        <table-block ref="secondBlock" @set-new-letter="letters.second = $event"></table-block>
        <table-block ref="thirdBlock" @set-new-letter="letters.third = $event"></table-block>
      </tr>
    </table>
    <button id="roll-btn" @click="createRoll" :disabled="isRollButtonDisabled">new roll</button>
  </div>
</template>

<script>
import TableBlock from "./TableBlock.vue";

export default {
  name: "CasinoTable.vue",
  components: {TableBlock},
  data() {
    return {
      score: 10,
      isResultLoading: false,
      letters: {
        first: null,
        second: null,
        third: null
      }
    }
  },
  computed: {
    isRollButtonDisabled() {
      return this.isResultLoading
    }
  },
  methods: {
    createRoll() {
      this.isResultLoading = true
      this.$refs.firstBlock.reRoll()
      this.$refs.secondBlock.reRoll()
      this.$refs.thirdBlock.reRoll()
      this.$refs.firstBlock.showLetterWithDelay(1000)
      this.$refs.secondBlock.showLetterWithDelay(2000)
      this.$refs.thirdBlock.showLetterWithDelay(3000).then(() => {
        this.checkTheResult()
        this.isResultLoading = false
      })
    },
    checkTheResult() {
      if(this.letters.first?.name === this.letters.second?.name &&
          this.letters.second?.name === this.letters.third?.name
      ) {
        // user has won the game
        this.giveUserScore(this.letters)
      } else {
        // user has failed
        this.reduceScore()
      }
    },
    giveUserScore(letters) {
      let score = letters.first.score
      this.score += score
    },
    reduceScore() {
      this.score--
    },
  }
}
</script>

<style scoped lang="scss">
.d-flex {
  display: flex;
}
#roll-btn {
  background: transparent;
  border: 1px solid white;
  margin-top: 3rem;
  font-size: 2rem;
  text-transform: uppercase;
  padding: 0.3em .6em;
  border-radius: 1rem;
  &:hover {
    background: rgba(255, 255, 255, 0.38);
  }
}
.score {
  margin-bottom: 3rem;
  font-size: 5rem;
}
</style>