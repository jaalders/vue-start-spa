<template>
  <div class="container mb-3">
    <form action="">
      <div class="mb-3">
        <label for="" class="form-label"> Page Title </label>
        <input type="text" class="form-control" v-model="pageTitle" />
      </div>
      <div class="mb-3">
        <label for="" class="form-label"> Content </label>
        <textarea type="text" class="form-control" rows="5" v-model="content"></textarea>
      </div>
      <div class="col">
        <div class="mb-3">
          <label for="" class="form-label"> Link Text </label>
          <input type="text" class="form-control" v-model="linkText" />
        </div>
        <div class="mb-3">
          <label for="" class="form-label"> Link URL </label>
          <input type="text" class="form-control" v-model="linkUrl" />
        </div>
      </div>
      <div class="row mb-3">
        <div class="form-check">
          <input class="form-check-input" type="checkbox" v-model="published" />
          <label class="form-check-label" for="gridCheck1"> Published </label>
        </div>
      </div>
      <div class="mb-3">
        <button class="btn btn-primary" :disabled="isFormInvalid" @click.prevent="submitForm">Create Page</button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import type { Page } from '@/models/page.models'

export default {
  props: ['pageCreated'],
  data() {
    return {
      pageTitle: '',
      content: '',
      linkText: '',
      linkUrl: '',
      published: false
    }
  },
  computed: {
    // computed properties simply return a value. They use the existing data in order to compute a value that is then used in the template. It does not affect the state.
    isFormInvalid() {
      return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl
    }
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert('Please fill out all form fields')
        return
      }

      this.$emit('pageCreated', {
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText,
          url: this.linkUrl
        },
        published: this.published
      })

      this.pageTitle = ''
      this.content = ''
      this.linkText = ''
      this.linkUrl = ''
      this.published = false
    }
  },
  watch: {
    // watch, watches for a property to change and then updated the state
    pageTitle(newTitle, oldTitle) {
      if (this.linkText === oldTitle) {
        this.linkText = newTitle
      }
    }
  },
  emits: {
    pageCreated(pageObj: Page) {
      if (!pageObj.pageTitle) {
        return false
      }

      if (!pageObj.content) {
        return false
      }

      if (!pageObj.link || !pageObj.link.text || !pageObj.link.url) {
        return false
      }
    }
  }
}
</script>
