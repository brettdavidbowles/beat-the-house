<template>
  <div>
    <div 
      v-if="!showNav"
      class="bg-black p-16 absolute w-full"
      />
    <div
      v-if="!showNav"
      class="p-4 relative"
    />
    <Header
      class="sticky top-0"
      @fullPageNav="toggleFullPageNav"
    />
    <TopBets
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