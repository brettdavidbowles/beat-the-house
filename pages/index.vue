<template>
  <div class="h-screen">
    <Header
      @fullPageNav="toggleFullPageNav"
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
