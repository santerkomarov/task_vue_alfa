<template>
  <HeaderComponent />
  <FirstPage/>
</template>

<script>
import HeaderComponent from './components/HeaderComponent'
import FirstPage from './components/FirstPage'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    FirstPage
  }
}
</script>

<style>
#app {
  padding: 0;
  margin: 0;
}
</style>
