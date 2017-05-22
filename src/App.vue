<template>
  <div id="app">
    <h1>Some examples of v-buttons and its current features</h1>
	<div>
		<v-button>Button with added CSS classes</v-button>
    	<v-button css-classes="primary">Button with added CSS classes</v-button>
    	<v-button css-classes="info" :throttled="true">Throttled button (default cooldown)</v-button>
    	<v-button css-classes="danger" :throttled="true" :cooldown="2000">Throttled button (longer cooldown)</v-button>
	</div>
  </div>
</template>

<script>
import button from './components/Button/Button.vue'

export default {
  name: 'app',
  components: {
    'v-button':button
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
