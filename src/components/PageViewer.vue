<template>
  <div class="container">
    <h1>{{ page.pageTitle }}</h1>
    <p>{{ page.content }}</p>
  </div>
</template>

<script lang="ts">
import type { Page } from '@/models/page.models'

export default {
  props: {
    page: {
      type: Object,
      default(rawProps: Page) {
        return {
          pageTitle: '',
          content: ''
        }
      }
    }
  }
}
</script>
