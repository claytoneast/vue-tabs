<template>
  <div id="app">
    <img width="25%" src="./assets/logo.png">
    <tabs>
      <tab link-text='tab0' hash='20498023485'>
        tab 0 content
      </tab>

      <tab link-text='tab1' hash='2058329085'>
        tab 1 content
      </tab>

      <tab link-text='tab2 link' hash='90338388'>
        tab 2 content
      </tab>
    </tabs>
  </div>
</template>

<script>
import Tabs from './components/Tabs'
import Tab from './components/Tab'

export default {
	name: 'App',
	components: {
		Tabs,
		Tab
	}
}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
