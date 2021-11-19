<template lang="pug">
  div
    div 404 not found
    NuxtLink(to="/after") back
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class NotA extends Vue {}
</script>
