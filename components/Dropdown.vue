<template>
  <div
    @mouseover="showDropDown = true"
    @mouseleave="showDropDown = false"
    class="relative z-50"
  >
    <button>
      {{ title }}
    </button>
    <div 
      v-if="showDropDown"
      class="w-56 p-2 flex flex-col absolute text-right right-2 bg-black"
    >
      <div
        v-for="link in links"
        :key="link.value"
      >
        <NuxtLink :to="link.value">{{ link.title }}</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    links: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      showDropDown: false,
    }
  }
}
</script>
