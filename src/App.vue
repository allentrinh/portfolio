<template>
  <div id="app">
    <MobileNavigation :mobileNavActive="mobileNavActive" v-on:mobileNavActive="toggleMobileNavActive($event)"/>
    <HeaderComponent :mobileNavActive="mobileNavActive" v-on:mobileNavActive="toggleMobileNavActive($event)"/>
    <main id="content">
      <transition name="router-animation" mode="out-in" enter-active-class="animated fadeIn" leave-active-class="animated fadeOut" :duration="200">
        <router-view/>
      </transition>
    </main>
    <FooterComponent v-if="!isHome"/>
  </div>
</template>

<script>
import MobileNavigation from '@/components/MobileNavigation.vue';
import HeaderComponent from '@/components/HeaderComponent.vue';
import FooterComponent from '@/components/FooterComponent.vue';

export default {
  name: 'App',
  components: {
    MobileNavigation,
    HeaderComponent,
    FooterComponent,
  },
  data() {
    return {
      mobileNavActive: false,
      isHome: Boolean,
    };
  },
  methods: {
    toggleMobileNavActive(isActive) {
      this.mobileNavActive = isActive;
    },
    checkHome() {
      this.isHome = this.$route.name === 'home';
    },
    isDesktop() {
      return window.innerWidth > 767;
    },
    resize() {
      if (this.isDesktop()) {
        this.mobileNavActive = false;
      }
    },
  },
  mounted() {
    this.checkHome();

    window.addEventListener('resize', this.resize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resize);
  },
  updated() {
    window.scrollTo(0, 0);
    this.checkHome();
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles.scss';

#app {
  position: relative;
}
</style>
