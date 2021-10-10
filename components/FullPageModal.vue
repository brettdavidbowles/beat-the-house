<template>
  <div>
    <div class="flex justify-between p-8">
      <h1 class="text-3xl px-3">Beat the House with AI</h1>
      <button 
        class="text-3xl"
        @click="close"
      >
        &#x2715;
      </button>
    </div>
    <div class="relative">
      <div class="absolute inset-0 w-screen h-screen bg-white p-8 transition-all ease-in-out duration-1000 transform translate-x-0 slide">
        <div class="flex flex-col w-full items-center text-center text-5xl py-2">
          <NuxtLink 
            v-for="link in links"
            :key="link.value"
            :to="link.value"
            class="p-6"
          >
            {{ link.title }}
          </NuxtLink>
          <button
            v-for="(link, index) in linkGroups"
            :key="link.category"
            class="p-6"
            @click="nextSlide(index)"
          >
            {{ link.category }}
            <span class="inline-block transform rotate-45 text-4xl">
              <span class="inline-block transform rotate-180">
                &#8735;
              </span>
            </span>
          </button>
        </div>
      </div>
      <div 
      class="absolute inset-0 w-screen h-screen bg-white flex flex-col items-center text-5xl transition-all ease-in-out duration-1000 transform translate-x-full slide">
        <button
          @click="previousSlide"
          class="p-6 flex items-center text-gray-400"
        >
          <span class="inline-block transform rotate-45 text-4xl">
            &#8735;
          </span>
          Back
        </button>
        <NuxtLink
          v-for="link in linkGroups[activeGroupIndex].links"
          :key="link.value"
          :to="link.value"
          class="p-6 text-center"
        >
          {{ link.title }}
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    links: {
      type: Array,
      required: false
    },
    linkGroups: {
      type: Array,
      required: false
    },
  },
  emits: [ 'close' ],
  data() {
    return {
      activeGroupIndex: 0
    }
  },
  methods: {
    close() {
      this.$emit('close')
    },
    nextSlide(index) {
      let activeSlide = document.querySelector('.slide.translate-x-0');
      activeSlide.classList.remove('translate-x-0');
      activeSlide.classList.add('-translate-x-full');
      
      let nextSlide = activeSlide.nextElementSibling;
      nextSlide.classList.remove('translate-x-full');
      nextSlide.classList.add('translate-x-0');

      this.setActiveGroupIndex(index)
    },
    previousSlide() {
      let activeSlide = document.querySelector('.slide.translate-x-0');
      activeSlide.classList.remove('translate-x-0');
      activeSlide.classList.add('translate-x-full');
      
      let previousSlide = activeSlide.previousElementSibling;
      previousSlide.classList.remove('-translate-x-full');
      previousSlide.classList.add('translate-x-0');
    },
    setActiveGroupIndex(groupIndex) {
      this.activeGroupIndex = groupIndex
    }
  }
}
</script>