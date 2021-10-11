<template>
  <div>
    <div class="bg-black p-16 absolute w-full" />
    <div class="p-4 relative" />
    <Header
      class="sticky top-0"
      @fullPageNav="toggleFullPageNav"
    />
    <NflOverUnder
      v-if="!showNav"
      class="py-12"
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