<template >

<main main class="align-items-center">

  <transition name="fade">
    <div class="pt-5" v-if="content=='main'">

      <transition name="fade">
        <b-jumbotron
          fluid
          container-fluid
          v-if="showWelcomeMessage"
          bg-variant="info"
          text-variant="white"
          border-variant="dark"
          header-level='1'
          class="w-75 mx-auto">
          <template slot="header">
            Tirrana
          </template>
          <template slot="lead">
            Welcome to Tirrana, to learn more about how this app works choose one the links below.
          </template>
          <hr class="my-4">
          <p class="mb-4">
            We bundle all your sources, notes, links to provide you a complete and immersive learning experience.
            No more notes, notebooks, documents strewn all over your computer. Keep everything in one place. Link topics and track
            your progess over time.
          </p>
          <p class="pl-4">
            <b-form-checkbox v-model="hideTutorial" @change="$emit('toggleTutorial', hideTutorial)"> </b-form-checkbox>Do not this message in the future.
          </p>
          <div class="">
            <b-button-close @click="showWelcomeMessage = !showWelcomeMessage">Close</b-button-close>
          </div>
        </b-jumbotron>
      </transition>
    </div>
  </transition>

  <transition name="fadeDown">
    <app-study-timer v-if="showStudyTimer"></app-study-timer>
  </transition >
</main>
</template>

<script>
import AppstudyTimer from './AppstudyTimer';

export default {
  name: 'AppmaincontenT',
  props: {
    showStudyTimer: Boolean,
    content : String,
    hideTutorial: Boolean,
  },
  components: {
      'app-study-timer': AppstudyTimer,
    },
  data: function(){
    return {
      showWelcomeMessage : true,
    }
  },
  created : function(){
    this.showWelcomeMessage = !this.hideTutorial;
  },
}
</script>

<style scoped>

  main {
    width: 100%;
    height: 100%;
    position: relative;
    transition: all .4s;
  }

</style>
