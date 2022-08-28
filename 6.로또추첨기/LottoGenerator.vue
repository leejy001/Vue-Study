<template>
  <div>
    <div>당첨 숫자</div>
    <div id="결과창">
      <lotto-ball v-for="ball in winBalls" :key="ball" :number="ball"></lotto-ball>
    </div>
    <div>보너스</div>
    <lotto-ball v-if="bonus" :number="bonus"></lotto-ball>
    <button v-if="redo" @click="onClickRedo">한 번 더!</button>
  </div>
</template>

<script>
import LottoBall from './LottoBall'

  function getWinNumbers() {
    const candidiate = Array(45).fill().map((v, i) => i + 1)
    const shuffle = []
    while(candidiate.length > 0) {
      shuffle.push(candidiate.splice(Math.floor(Math.random() * candidiate.length), 1)[0])
    }
    const bonusNumber = shuffle[shuffle.length - 1];
    const winNumbers =shuffle.slice(0, 6).sort((p, c) => p - c)
    return [...winNumbers, bonusNumber]
  }
  const timeouts = []
  export default {
    components: { 
      LottoBall 
    },
    data() {
      return {
        winNumbers: getWinNumbers(),
        winBalls: [],
        bonus: null,
        redo: false,
      }
    },
    computed: {

    },
    methods: {
      onClickRedo() {
        this.winNumbers = getWinNumbers()
        this.winBalls = []
        this.bonus = null
        this.redo = false
        this.showBalls()
      },
      showBalls() {
        for(let i = 0; i < this.winNumbers.length - 1; i++) {
          timeouts[i] = setTimeout(() => {
            this.winBalls.push(this.winNumbers[i])
          }, (i + 1) * 1000)
        }
        timeouts[6] = setTimeout(() => {
          this.bonus = this.winNumbers[6]
          this.redo = true
        }, 7000)
      }
    },
    mounted() {
      this.showBalls()
    },
    beforeDestory() {
      timeouts.forEach((t) => {
        clearTimeout(t)
      })
    },
    watch: { // 어떤 값이 변경되었는지 감시하고 메서드를 실행할 수 있음 (웬만하면 사용하지 않는 것을 추천)
      // winBalls(val, oldVal) {
      //   if(val.length === 0) {
      //     this.showBalls();
      //   }
      // }
    } 
  }
</script>

<style scoped>

</style>
