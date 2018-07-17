<template>
	<transition :name='animationName'>
		<div v-if='active' class='tab-wrapper'>
			<h1>Tab Content {{ linkText }}</h1>
			<slot>
        Default Slot Content
			</slot>
		</div>
	</transition>
</template>

<script>
export default {
  props: {
    hash: { required: true, type: String },
    linkText: { required: true, type: String }
  },
  data: function() {
    return {
      active: false,
      animationName: ''
    }
  },
  inject: ['currentTab'],
  watch: {
    'currentTab.hash': function() {
      this.animationName = `pane-${this.currentTab.animationDirection}`
      this.$nextTick(() => {
        this.active = this.currentTab.hash === this.hash
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.tab-wrapper {
  background: white;
  min-height: 380px;
  position: absolute;
  top: 0;
  left: 20px;
  width: calc(100% - 44px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
}

.pane-left-enter-active,
.pane-right-enter-active {
  transition: transform 1s cubic-bezier(0, 1, 0.51, 1);
}
.pane-left-leave-active,
.pane-right-leave-active {
  transition: all 0.4s ease-in;
  z-index: 2;
}

.pane-left-leave-to {
  transform: translateX(-100%);
}

.pane-right-leave-to {
  transform: translateX(100%);
}

.pane-left-enter,
.pane-right-enter {
  transform: scale(0.8);
}
</style>
