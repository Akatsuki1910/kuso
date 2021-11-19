<template lang="pug">
  div
    li
      a(href="https://u-site.jp/alertbox/ten-usability-heuristics") ヤコブの10ユーザビリティヒューリスティックス
      ul
        li システム状態の視認性
        li システムと実世界の一致
        li ユーザーの主導権と自由
        li 一貫性と標準
        li エラーの予防
        li 再生より再認
        li 柔軟性と効率性
        li 美的で最小限のデザイン
        li ユーザーによるエラーの認識・診断・回復のサポート
        li ヘルプとドキュメンテーション
    li ユーザビリティの定量化と指標
      ul
        li 作業時間
        li 作業の正確さ
        li 習得時間
        li 生理的負荷
        li 満足度
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class CheckList extends Vue {}
</script>
