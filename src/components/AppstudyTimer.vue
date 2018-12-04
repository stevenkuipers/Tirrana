<template >
  <nav class="timer" :style="{width : Computedwidth +'px'}">
    {{ hello }}
  </nav>
</template>

<script>
export default {
  name: 'AppstudyTimer',
  data : function(){
    return {
      width: '100',
      hello: 'Here we are going to put a timer '
    }
  },
  methods : {
    debounce: function(fn, wait) {
    let timeout;
    return function () {
      clearTimeout(timeout);
      timeout = setTimeout(() => fn.apply(this, arguments), (wait || 1));
    }
  }
  },
  mounted : function(){
      this.width = this.$el.parentNode.clientWidth;
      window.addEventListener('resize', this.debounce(function () {
        console.log('fire');
          this.width = this.$el.parentNode.clientWidth;
      }.bind(this), 200));
  },
  computed : {
    Computedwidth : function(){
      return this.width;
    }
  }

}
</script>

<style lang="css">
.timer {
  position: fixed;
  bottom: 0;
  right: 0;
  display: flex;
  flex: 1;
  align-items: center;
  justify-content: center;
  background: var(--info);
  height: 4rem;
  border-top: 1px solid var(--light);
  transition: width .2s;
}
</style>
