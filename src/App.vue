<template>
    <b-container fluid class="app__container" :style="{backgroundImage : bgImage}">

      <div :class="colWidth" class="col-fix-w" >
        <b-button block @click="toggleNav">{{ showNav ? 'Close' : 'Open' }} Menu</b-button>
        <!-- Custom transition / not with animate library -->
        <transition name="slide-to-the-left">
        <b-nav pills vertical class="pt-5 nav__menu bg-secondary" v-if="showNav">
          <b-nav-item @click="content = 'main'" class="pb-4" active>Main</b-nav-item>
          <b-nav-item @click="showStudyTimer = !showStudyTimer" class="pb-4" >Study Timer</b-nav-item>
          <b-nav-item @click="content = 'notes'" class="pb-4" >Notes</b-nav-item>
        </b-nav>
        </transition>
      </div>

      <app-main-content
        :hideTutorial="hideTutorial"
        :content="content"
        :showStudyTimer="showStudyTimer"
        v-on:toggleTutorial="toggleTutorial"
        ></app-main-content>

  </b-container>
</template>

<script>
import AppmenU from './components/AppmenU';
import AppmainContent from './components/AppmaincontenT';

export default {
  name: 'app',
  components: {
      'app-menu': AppmenU,
      'app-main-content': AppmainContent,
    },
  data () {
    return {
      user : {},
      showNav: true,
      hideTutorial : false,
      showStudyTimer : false,
      colWidthWide: 'col-fix-w-wide',
      colWidthSmall: 'col-fix-w-small',
      content : 'main',
      backgroundImages : ['background-image01.jpg', 'background-image02.jpg','background-image03.jpg'],
    }
  },
  created : function(){

    // On first initialization of app:
    if(!store.get('settings')){
      store.set('settings', { hideTutorial: false })
    }

    if(!store.get('name')){
      store.set('user', { name: '' })
    }


    //Get all stored data from localstorage and set data with it 
    this.hideTutorial = store.get('settings').hideTutorial;
    this.user = store.get('user').name;

  },
  computed : {
    colWidth : function(){
      return this.showNav ? this.colWidthWide : this.colWidthSmall
    },
    bgImage : function(){
      return 'url(./images/' +this.backgroundImages[0] + ')'
    },
  },
  methods : {
    toggleTutorial : function(val){
      this.hideTutorial = val;
      store.set('settings', { hideTutorial: true})
    },
    toggleNav : function(event){
      this.showNav = !this.showNav;
      let timeout;
      timeout = setTimeout( () => window.dispatchEvent(new Event('resize') ), 800);
    },
  }
}
</script>

<style>
  .app__container {
    padding-left: 0;
    padding-right: 0;
    display: flex;
    align-items: stretch;
    min-height: 100vh;
    background-image: url(./images/background-image01.jpg);
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
  }

.nav__side__open {
  width: 2.2rem;
  content: '';
  writing-mode: vertical-rl;
  text-orientation: upright;
  color: var(--secondary);
  cursor: pointer;
}

.col-fix-w {
  background: rgba(250,250,250,0.3);
  flex-grow: 0;
  flex-shrink: 0;
  max-width: 100%;
  transition: all .5s .3s;
}

/* Add coll override to fix width of navigation on left side */
.col-fix-w-wide {
  flex-basis: 18rem;
}
/* Add coll override to fix width of navigation on left side */
.col-fix-w-small {
  flex-basis: 2rem;
}

.main__content {
  justify-content: stretch;
}

.flex-grow {
  flex: 1 0 auto;
}

/* Enter and leave animations can use different */
/* durations and timing functions.              */
.slide-to-the-left-enter-active {
  width: 100%;
  transition: all .3s ease;
}
.slide-to-the-left-leave-active {
  width: 100%;
  transition: all .3s ease;
}
.slide-to-the-left-enter, .slide-to-the-left-leave-to {
  transform: translateX(-100px);
  width: 0;
  opacity: 0;
}
</style>
