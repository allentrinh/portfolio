<template>
  <header id="header">
    <div class="container is-fluid">
      <div class="columns is-mobile level-item">
        <div class="column is-narrow">
          <router-link to="/" class="logo">Allen Trinh</router-link>
        </div>
        <div class="column has-text-right">
          <nav class="navbar is-hidden-touch">
            <ul class="nav">
              <li><router-link to="/">Home</router-link></li>
              <li><router-link to="/about">About</router-link></li>
              <li><router-link to="/resume">Resumé</router-link></li>
              <li><router-link to="/work">Work</router-link></li>
              <li><router-link to="/contact">Contact</router-link></li>
            </ul>
          </nav>
          <button @click="toggleNav" :class="['mobile-nav-btn is-hidden-desktop', { active: mobileNavActive }]">
            <span></span>
            <span></span>
            <span></span>
          </button>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      mobileNavActive: false
    };
  },
  methods: {
    toggleNav() {
      console.log('hello');
      this.mobileNavActive = !this.mobileNavActive;
    }
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles.scss';

#header {
  background: -moz-linear-gradient(top, rgba(0,0,0,0.65) 0%, rgba(0,0,0,0) 100%);
  background: -webkit-linear-gradient(top, rgba(0,0,0,0.65) 0%,rgba(0,0,0,0) 100%);
  background: linear-gradient(to bottom, rgba(0,0,0,0.65) 0%,rgba(0,0,0,0) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#a6000000', endColorstr='#00000000',GradientType=0 );
  padding: 1em;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1;
}

.logo {
  font-size: 2rem;
  font-family: $font;
  color: #fff;
}

.mobile-nav-btn {
  background-color: transparent;
  border: 0;
  width: 40px;
  height: 36px;
  position: relative;
  outline: 0;
  cursor: pointer;
  &.active {
    span {
      &:first-child {
        transform: rotate(-45deg);
        transition: transform .45s cubic-bezier(0.9, -0.6, 0.3, 1.6) 0.1s;
      }
      &:nth-child(2) {
        width: 19px;
        transform: translate(6px, 0) rotate(45deg);
        transition: transform 0.45s cubic-bezier(0.9, -0.6, 0.3, 1.6) 0.1s, width 0.2s ease;
      }
      &:last-child {
        width: 19px;
        transform: translate(-6px, 0) rotate(45deg);
        transition: transform 0.45s cubic-bezier(0.9, -0.6, 0.3, 1.6) 0.1s, width 0.2s ease;
      }
    }
  }
  span {
    position: absolute;
    height: 4px;
    border-radius: 2px;
    background: #fff;
    transition: transform 0.45s cubic-bezier(0.9, -0.6, 0.3, 1.6), width 0.2s ease 0.2s;
    &:first-child {
      top: 50%;
      left: 0;
      margin: -2px 0 0 0;
      width: 40px;
      transform-origin: 50% 50%;
    }
    &:nth-child(2) {
      top: 2px;
      left: 0;
      width: 20px;
      transform-origin: 0 50%;
    }
    &:last-child {
      bottom: 2px;
      right: 0;
      width: 28px;
      transform-origin: 100% 50%;
      transform: translate(-12px, 0);
    }
  }
}

.navbar {
  background: transparent;
}

.nav {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 100%;
  li {
    padding: 0 1em;
  }
  a {
    color: #fff;
    padding: 0.5em 0;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-size: 0.85em;
    position: relative;
    &:hover {
      &::before {
        visibility: visible;
        transform: scaleX(1);
      }
    }
    &::before {
      content: '';
      display: block;
      position: absolute;
      width: 100%;
      height: 1px;
      bottom: 0;
      left: 0;
      background: $primaryColor;
      visibility: hidden;
      transform: scaleX(0);
      @include transition;
    }
  }
}
</style>