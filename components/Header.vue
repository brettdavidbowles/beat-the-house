<template>
  <div>
    <div 
      class="flex w-full items-center justify-between bg-black text-white sticky px-8 py-2.5"
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
    </div>
        <FullPageModal
          v-if="showFullPageNav"
          class="w-full h-full fixed z-10 left-0 top-0"
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
