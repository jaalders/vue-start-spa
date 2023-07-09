<template>
  <Navbar :pages="pages" :active-page="activePage" :nav-link-click="(index: number) => activePage = index"></Navbar>
  <CreatePage @page-created="pageCreated"> </CreatePage>
</template>

<style scoped></style>

<script lang="ts">
import PageViewer from './components/PageViewer.vue'
import Navbar from './components/Navbar.vue'
import CreatePage from './components/CreatePage.vue'
import type { Page } from '@/models/page.models'

export default {
  components: {
    PageViewer,
    Navbar,
    CreatePage
  },
  data() {
    return {
      activePage: 0,
      pages: [] as Page[]
    }
  },
  created() {
    this.getPages()
  },
  methods: {
    async getPages() {
      let res = await fetch('./src/stores/pages.json')
      let data = await res.json()

      this.pages = data
    },
    pageCreated(pageObj: Page): void {
      this.pages.push(pageObj)
    }
  }
}
</script>
