<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <Navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index: number) => activePage = index"
  ></Navbar>

  <div v-show="false">hide this content</div>

  <!-- <PageViewer v-if="pages.length > 0" :page="pages[activePage]"></PageViewer> -->
  <CreatePage :pageCreated="pageCreated"> </CreatePage>
  <!-- <RouterView /> -->
</template>

<style scoped></style>

<script lang="ts">
import PageViewer from './components/PageViewer.vue'
import Navbar from './components/Navbar.vue'
import CreatePage from './components/CreatePage.vue'

interface Page {
  pageTitle: string
  content: string
  linkText: string
  linkUrl: string
}

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
