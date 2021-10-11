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
    <div class="py-8">
      <slot v-if="!showNav"></slot>
    </div>
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
