<template lang="pug">
  div.bg
    h1.rainbow ガチャガチャ
    p
      div
        | 石
        span {{stone}}
      div
        span(@click="stone1").button 石1
        span(@click="stone10").button 石10
    p
      span(@click="gacha10").button ガチャ10
      span(@click="gacha1").button ガチャ1
      span(@click="reset").button リセット
    p
      div 結果
      div(v-for="(item,i) in result" :key="i") {{item}}
      div(v-for="(item,i) in Object.entries(data)" :key="i") {{item[0]}}:{{item[1]}}
    p
      div
        NuxtLink(to="/before/a" target="_blank") go to a
      div
        NuxtLink(to="/") back
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class Before extends Vue {
  stone = 0
  result: string[] = []
  data: { [key: string]: number } = {
    '★1': 0,
    '★2': 0,
    '★3': 0,
    '★4': 0,
    '★5': 0,
  }

  stone1() {
    this.stone += 1
  }

  stone10() {
    this.stone += 10
  }

  gacha1() {
    this.gachaN(1)
  }

  gacha10() {
    this.gachaN(10)
  }

  reset() {
    this.data = Object.fromEntries(
      Object.entries(this.data).map(([_, _value]) => [_, 0]),
    )
    this.result = []
  }

  gachaN(num: number) {
    const s = num * 5
    if (this.stone >= s) {
      this.stone -= s
      this.result = []
      for (let i = 0; i < num; i++) {
        this.gacha()
      }
    }
  }

  gacha() {
    // 1 5
    // 2 2
    // 3 1.5
    // 4 1
    // 5 0.5
    const m = Math.random()
    const r = m > 0.5 ? 1 : m > 0.2 ? 2 : m > 0.15 ? 3 : m > 0.1 ? 4 : 5
    const s = `★${r}`
    this.result.push(s)
    this.data[s]++
  }
}
</script>

<style lang="scss" scoped>
.bg {
  background: crimson;
  user-select: none;
}

.button {
  border: 1px black solid;
}

.rainbow {
  background: linear-gradient(
      to right,
      #f00 0%,
      #f80 14.28%,
      #dd0 28.56%,
      #0d0 42.85%,
      #0dd 57.14%,
      #00f 71.42%,
      #e0e 85.71%,
      #f00 100%
    )
    0% center / 200% auto;
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  animation: bggradient 2s linear infinite;
}

@keyframes bggradient {
  0% {
    background-position: 0% 0%;
  }
  50% {
    background-position: 100% 0%;
  }
  100% {
    background-position: 200% 0%;
  }
}
</style>
