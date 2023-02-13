<template>
  <div>
    <button id="cash-out" @mouseover="translateRandomly($event)">cash out</button>
  </div>
</template>

<script>
export default {
  name: "CashOutBtn.vue",
  methods: {
    translateRandomly(e) {
      let chance = Math.random()
      if(chance <= .5) {
        let direction = ['+', '-'][Math.floor(Math.random() * 2)]
        e.target.style.transform = `translateX(${direction}300px)`
      }
    }
  }
}
</script>

<style scoped>
#cash-out {
  transition: transform .2s ease-in-out;
}
</style>