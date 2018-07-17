<template>
  <div id="app">
    <img width="25%" src="./assets/logo.png">
    <tabs>
      <div slot='tabs'>
        <tab key='20498023485' link-text='tab0' hash='20498023485'>
          <div slot='body'>
            tab 0 content
          </div>
        </tab>

        <tab key='2058329085' link-text='tab1' hash='2058329085'>
          <div slot='body'>
            tab 1 content
          </div>
        </tab>

        <tab key='90338388' link-text='tab2 link' hash='90338388'>
          <div slot='body'>
            tab 2 content
          </div>
        </tab>
      </div>

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
