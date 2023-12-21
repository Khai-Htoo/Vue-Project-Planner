<template>
  <div>
    <NavBar class=" text-center "></NavBar>
<router-view></router-view>
  </div>
</template>

<script>
  import NavBar from './components/NavBar'
export default {
  components: { NavBar },
    
  }
</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 800px;
  margin: auto;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

a {
  font-weight: bold;
  color: #2c3e50;
}

a.router-link-exact-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>
