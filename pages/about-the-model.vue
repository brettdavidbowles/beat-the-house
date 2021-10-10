<template>
  <div>
    <Header
      @fullPageNav="toggleFullPageNav"
    />
    <AboutTheModel
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
