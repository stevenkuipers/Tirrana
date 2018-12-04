<template >
  <nav class="menu">
    {{ hello}}
  </nav>
</template>

<script>
export default {
  name: 'AppmenU',
  data: function(){
    return {
      hello: 'Hello here'
    }
  }

}
</script>

<style lang="css">
.menu {
  background: rgba(250,250,250,0.15);
  width: 100%;
  /* min-height: 100vh; */
}
</style>
