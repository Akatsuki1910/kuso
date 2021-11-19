<template lang="pug">
  div
    NuxtLink(to="/before/a") go to a
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class Before extends Vue {}
</script>
