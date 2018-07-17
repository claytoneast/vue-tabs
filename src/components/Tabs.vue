<template>
  <div class='tabs'>
    <h2>Tabs Root Level</h2>
    <div class='nav-wrapper'>
      <div class='nav-inner'>
        <a
          class='nav-link' 
          v-for='(tab, index) in tabs'
          :key='tab.hash'
          @click.prevent='updateCurrentTab(tab.hash)'
        >
         {{index}} {{ tab.linkText }}
        </a>
        <div class='nav-marker'>
        </div>
      </div>
    </div>

    <div class='panes-wrapper'>
      <slot name='tabs'>
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  props: ['direction'],

  data: function() {
    return {
      tabs: [],
      activeHash: '',
      animationDirection: 'left'
    }
  },

  methods: {
    updateCurrentTab: function(newHash) {
      const nextIndex = this.tabs.findIndex(tab => tab.hash === newHash)
      const prevIndex = this.tabs.findIndex(tab => tab.hash === this.activeHash)
      this.animationDirection = (nextIndex > prevIndex ? 'left' : 'right')
      this.$nextTick(() => {
        this.activeHash = newHash
        this.positionMenuMarker()
      })
    },

    positionMenuMarker: async function() {
      await this.$nextTick()
      const activeIndex = this.tabs.indexOf(
        this.tabs.find(tab => tab.hash === this.activeHash)
      )
      const navLinks = document.getElementsByClassName('nav-link')
      const activeLink = navLinks[activeIndex]
      const linkWidth = activeLink.offsetWidth
      const linkOffset = activeLink.offsetLeft
      const marker = document.getElementsByClassName('nav-marker')[0]
      marker.style.transform = `translateX(${linkOffset}px)`
      marker.style.width = `${linkWidth}px`
    }
  },

  provide() {
    const currentTab = {}
    Object.defineProperties(currentTab, {
      hash: {
        enumerable: true,
        get: () => this.activeHash
      },
      animationDirection: {
        enumerable: true,
        get: () => this.animationDirection
      }
    })
    return { currentTab }
  },

  // watch: {
  //   activeHash: function(next, prev) {
  //     this.positionMenuMarker()
  //   }
  // },

  mounted() {
    this.tabs = this.$children.map(tab => {
      return {
        hash: tab.hash,
        linkText: tab.linkText
      }
    })
    this.activeHash = this.tabs[0].hash
    this.updateCurrentTab(this.activeHash)
    this.positionMenuMarker()
  }
}
</script>

<style lang="scss" scoped>
.tabs {
  background: purple;
}

.nav-link {
  background: blue;
  color: white;
  padding: 15px 20px 15px 20px;
  min-width: 120px;
}

.nav-inner,
.nav-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;
  align-items: center;
  position: relative;
}

.nav-marker {
  height: 3px;
  background: magenta;
  position: absolute;
  left: 0;
  bottom: 0;
  width: 40px;
  transition: width 0.2s ease-out, transform 0.3s ease;
}

.panes-wrapper {
  position: relative;
  height: 400px;
}
</style>
