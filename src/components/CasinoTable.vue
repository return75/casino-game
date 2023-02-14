<template>
  <div>
    <div class="score">SCORE: {{score}}</div>
    <table>
      <tr class="d-flex">
        <table-block ref="firstBlock" @set-new-letter="letters.first = $event" />
        <table-block ref="secondBlock" @set-new-letter="letters.second = $event" />
        <table-block ref="thirdBlock" @set-new-letter="letters.third = $event" />
      </tr>
    </table>
    <div>
      <button id="roll-btn" @click="createRoll" :disabled="isRollButtonDisabled">new roll</button>
    </div>
    <cash-out-btn />
  </div>
</template>

<script>
import TableBlock from "./TableBlock.vue";
import CashOutBtn from "./CashOutBtn.vue";

export default {
  name: "CasinoTable.vue",
  components: {TableBlock, CashOutBtn},
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
      this.reRoll().then(() => {
        this.checkTheResult()
      })
      this.showLettersWithDelay().then(() => {
        this.isResultLoading = false
      })
    },
    reRoll() {
      return new Promise(resolve => {
        this.$refs.firstBlock.reRoll()
        this.$refs.secondBlock.reRoll()
        this.$refs.thirdBlock.reRoll()
        resolve()
      })
    },
    showLettersWithDelay() {
      return new Promise(resolve => {
        this.$refs.firstBlock.showLetterWithDelay(1000)
        this.$refs.secondBlock.showLetterWithDelay(2000)
        this.$refs.thirdBlock.showLetterWithDelay(3000).then(() => {
          resolve()
        })
      })
    },
    checkTheResult() {
      if(this.letters.first?.name === this.letters.second?.name &&
          this.letters.second?.name === this.letters.third?.name
      ) {
        // user has won the game
        if(this.score < 40) {
          this.giveUserScore()
        } else if (this.score >= 40 && this.score < 60) {
          let chance = Math.random()
          if(chance <= .3) {
            this.reRoll().then(() => {
              this.checkTheResult()
            })
          } else {
            this.giveUserScore()
          }
        } else {
          let chance = Math.random()
          if(chance <= .6) {
            this.reRoll().then(() => {
              this.checkTheResult()
            })
          } else {
            this.giveUserScore()
          }
        }
      } else {
        // user has failed
        this.reduceScore()
      }
    },
    giveUserScore() {
      this.showLettersWithDelay().then(() => {
        let score = this.letters.first.score
        this.score += score
      })
    },
    reduceScore() {
      this.showLettersWithDelay().then(() => {
        this.score--
      })
    },
  }
}
</script>

<style lang="scss">
.d-flex {
  display: flex;
}
#roll-btn, #cash-out {
  &:hover {
    background: rgba(255, 255, 255, 0.38);
  }
}
.score {
  margin-bottom: 3rem;
  font-size: 5rem;
}
</style>