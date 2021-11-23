<template lang="pug">
  div.bg
    h1 ガチャガチャ
    p
      div
        | 石:
        span {{stone}}
      div
        input(type="button" @click="stone1" value=" 石を1個足す")
        input(type="button" @click="stone10" value=" 石を10個足す")
    p
      input(type="button" @click="gacha1" value="1回回す")
      input(type="button" @click="gacha10" value="10回回す")
    p
      input(type="button" @click="reset" value=" リセット")
    p
      div 結果
      div(v-for="(item,i) in result" :key="i") {{item}}
      div(v-for="(item,i) in Object.entries(data)" :key="i") {{item[0]}}:{{item[1]}}
    p
      div
        NuxtLink(to="/after/a") go to a
      div
        NuxtLink(to="/") back
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class After extends Vue {
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
    if (window.confirm('削除しますか？')) {
      this.data = Object.fromEntries(
        Object.entries(this.data).map(([_, _value]) => [_, 0]),
      )
      this.result = []
    }
  }

  gachaN(num: number) {
    const s = num * 5
    if (this.stone >= s) {
      this.stone -= s
      this.result = []
      for (let i = 0; i < num; i++) {
        this.gacha()
      }
    } else {
      window.alert(`石があと、${s - this.stone}個足りません`)
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
