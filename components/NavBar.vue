<template>
  <div class="flex items-center">
    <div 
      class="flex items-center"
      v-for="link in links"
      :key="link.value"
    >
      <div class="px-2">
        <NuxtLink :to="link.value">{{ link.title }}</NuxtLink>
      </div>
    </div>
    <div v-for="dropdownLink in dropdownLinks" :key="dropdownLink.category">
      <Dropdown
      :title="dropdownLink.category"
      :links="dropdownLink.links"
      class="px-2"/>
    </div>
    <NuxtLink 
      to="/contact"
      class="py-3 px-5 bg-white text-black">
      Contact Us
    </NuxtLink>
  </div>
</template>

<script>

export default {
  props: {
    links: {
      type: Array,
      required: false
    },
    dropdownLinks: {
      type: Array,
      required: false
    }
  }
}
</script>

