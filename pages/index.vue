<template lang="pug">
  div
    div
      NuxtLink(to="/before") before
    div
      NuxtLink(to="/after") after
    CheckList
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class Index extends Vue {}
</script>
