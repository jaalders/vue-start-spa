<template>
  <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar navbar-expand-lg']">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">My Vue</a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <NavbarLink
          v-for="(page, index) in publishedPages"
          class="nav-item"
          :page="page"
          :isActive="activePage == index"
          :key="index"
          @click.prevent="navLinkClick(index)"
        >
        </NavbarLink>
      </ul>
      <form class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme()">Toggle Navbar</button>
      </form>
    </div>
  </nav>
</template>

<script lang="ts">
import NavbarLink from './NavbarLink.vue'
export default {
  props: ['pages', 'activePage', 'navLinkClick'],
  data() {
    return {
      theme: 'light'
    }
  },
  components: {
    NavbarLink
  },
  created() {
    this.getThemeSetting()
  },
  computed: {
    publishedPages() {
      return this.pages.filter((p: { published: boolean }) => p.published)
    }
  },
  methods: {
    changeTheme() {
      let theme = 'light'

      if (this.theme == 'light') {
        theme = 'dark'
      }

      this.theme = theme
      this.storeThemeSetting()
    },
    storeThemeSetting() {
      localStorage.setItem('theme', this.theme)
    },
    getThemeSetting() {
      let theme = localStorage.getItem('theme')

      if (theme) {
        this.theme = theme
      }
    }
  }
}
</script>
