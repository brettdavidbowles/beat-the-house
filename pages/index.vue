<template>
  <div class="h-screen">
    <Header
      @fullPageNav="toggleFullPageNav"
      class="sticky top-0"
    />
    <Home
      v-if="!showNav"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      showNav: false
    }
  },
  methods: {
    toggleFullPageNav() {
      this.showNav = !this.showNav
    }
  }
}
</script>
