<template>
  <div>
    <div 
      class="flex items-center justify-between bg-black text-white sticky p-8"
      v-if="!showFullPageNav"
    >
      <h1 class="text-3xl px-3">Beat the House with AI</h1>
      <NavBar 
        v-if="mediumScreenBreakPoint"
        :links="links"
        :dropdownLinks="dropdownLinks"
      />
      <button
        v-else
        @click="toggleFullPageNav"
      >
        <img src="~/assets/svg-menu-icon-3.svg"
          height="20"
          width="20"
        />
      </button>
      <!-- <div 
      class="flex items-center"
      v-if="mediumScreenBreakPoint"
      >
        <div v-for="link in links" :key="link.value">
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
      </div> -->
    </div>
  <FullPageModal
    v-else
    :links="links"
    :linkGroups="dropdownLinks"
    @close="toggleFullPageNav"
  />
  </div>
</template>

<script>

export default {
  emits: [ 'fullPageNav' ],
  data() {
    return {
      links: [
        { title: 'Home', value: '/' },
        { title: 'About the Model', value: '/about-the-model' },
        { title: 'Top Bets', value: '/topbets' }
      ],
      dropdownLinks: [
        { category: 'NFL Picks',
          links: [
            { title: 'NFL Spread', value: '/nfl-spread' },
            { title: 'NFL Over-Under', value: '/nfl-overunder' },
            { title: 'Receiving Yards', value: '/wr-stats' },
            { title: 'Rushing Yards', value: 'rb-stats' }
          ]
        },
        { category: 'NBA Picks',
          links: [
            { title: 'NBA Spread', value: '/nba-spread' },
            { title: 'NBA Over-Under', value: '/nba-overunder' },
            { title: 'Points', value: '/points' },
            { title: 'Rebouds', value: 'rebounds' },
            { title: 'Assists', value: 'assists' }
          ]
        }
      ],
      screenSize: 0,
      showFullPageNav: false
    }
  },
  computed: {
    mediumScreenBreakPoint() {
      return this.screenSize > 962
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.reportWindowSize()
      window.addEventListener('resize', this.reportWindowSize)
    })
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.reportWindowSize)
  },
  methods:{
    reportWindowSize() {
      this.screenSize = window.innerWidth
    },
    toggleFullPageNav() {
      this.showFullPageNav = !this.showFullPageNav
      this.$emit('fullPageNav')
    }
  }
}
</script>