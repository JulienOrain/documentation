<template>
  <header class="header" @keyup.esc="hideSearch">
    <div v-if="displayHeaderMessage" class="header__message">
      <div class="container">
        <p>
          We've updated Reliably's manifest structure. <g-link to="/guides/how-it-works/migrate-manifest/">Discover how to update your existing manifests.</g-link> <button @click="discardHeaderMessage"><span class="screen-reader-text">Discard this message></span><IconClose /></button>
        </p>
      </div>
    </div>
    <div class="container">
      <div class="header__logo">
        <a href="/" class="header-logo">
          <ReliablyLogo />
          <span class="screen-reader-text">Reliably</span>
        </a>
        <g-link class="header-docs-home" to="/">docs</g-link>
        {{ currentMode }}
      </div>
      <nav class="nav">
        <g-link class="nav__link" to="/getting-started/">Getting Started</g-link>
        <g-link class="nav__link" to="/guides/">Guides</g-link>
        <g-link class="nav__link" to="/reference/">Reference</g-link>
      </nav>
      <button
        @click.stop="displaySearch"
        class="header__search button button--icon button--secondary">
        Search the docs...
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-search"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
      </button>
    </div>
    <div v-show="isSearchDisplayed" class="algolia-search">
      <LazyHydrate on-interaction>
        <SearchComponent
          @close-search="hideSearch"
        />
      </LazyHydrate>
    </div>
  </header>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import ReliablyLogo from '@/assets/images/reliably-logo.svg';
import IconClose from '~/assets/images/icons/x.svg';
import SearchComponent from '~/components/SearchComponent.vue';

import LazyHydrate from 'vue-lazy-hydration';

export default {
  components: {
    ReliablyLogo,
    IconClose,
    SearchComponent,
    LazyHydrate,
  },
  data() {
    return {
      displayHeaderMessage: false,
      isSearchDisplayed: false,
    }
  },
  mounted() {
    // Put this back when we need to display a header message again
    // if (localStorage.getItem("reliablyDisplayHeaderMessage") === null) {
    //   localStorage.reliablyDisplayHeaderMessage = true;
    // } else if (localStorage.reliablyDisplayHeaderMessage === "false") {
    //   // because localStorage only stores strings...
    //   this.displayHeaderMessage = false;
    // } else if (localStorage.reliablyDisplayHeaderMessage === "true") {
    //   this.displayHeaderMessage = true;
    // }

    // ...and comment this
    localStorage.removeItem('reliablyDisplayHeaderMessage');
  },
  methods: {
    discardHeaderMessage() {
      this.displayHeaderMessage = false;
      localStorage.reliablyDisplayHeaderMessage = false;
    },
    displaySearch() {
      this.isSearchDisplayed = true;
      document.body.classList.add("no-scroll");
    },
    hideSearch() {
      this.isSearchDisplayed = false;
      document.body.classList.remove("no-scroll");
    }
  }
}
</script>

<style lang="scss">
.header {
  position: sticky;
  top: 0;
  z-index: 20;

  display: flex;
  flex-direction: column;
  align-items: center;
  height: auto;
  padding: .2em 0;

  background-color: var(--blue-800);

  // @media screen and (min-width: 39.5rem) {
  //   padding-bottom: 0;
  // }

  &__message {
    width: 100%;

    background-color: var(--red-500);

    color: white;
    text-align: center;

    p {
      margin-top: .5rem;
      margin-bottom: .5rem;
      width: 100%;
    }

    a {
      color: var(--yellow-300);
    }

    button {
      margin-left: 1.6rem;
      background-color: transparent;
      border: none;
      cursor: pointer;

      color: white;

      svg {
        height: 1.6rem;
        width: 1.6rem;

        vertical-align: -.3rem;

        stroke-width: 4;
      }
    }
  }

  .container {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    max-width: 124rem;
    padding-right: 2rem;
    padding-left: 2rem;

    @media (min-width: 50em) {
      flex-direction: row;
    }
  }
  &__logo {
    display: flex;
    align-items: center;

    .header-logo {
      display: flex;
      align-items: center;

      svg {
        height: 2em;
      }
    }

    .header-docs-home {
      position: relative;

      display: inline-block;
      height: 1.8rem;
      margin-left: .4em;
      padding: 0 .3em;

      background-color: var(--yellow-500);
      border-radius: .2rem;

      color: var(--heading-color);
      font-size: 1.2rem;
      // font-family: 'Agrandir', sans-serif;
      // font-weight: 700;
      text-decoration: none;
      text-transform: uppercase;

      transform: translateY(.2rem);
      transition: all .1s ease-in-out;

      &:hover {
        transform: scale(1.1) translateY(.2rem);
      }
    }
  }

  nav {
    margin-right: auto;
    margin-left: auto;
    @media screen and (min-width: 40rem) {
      // margin-left: 0;
    }
    a {
      position: relative;

      display: inline-block;
      padding: 1.2rem;

      color: white;
      font-weight: 700;
      text-decoration: none;

      @media (min-width: 30rem) {
        margin: 0 .5em;
        padding: 1em;
      }

      &:hover,
      &.active {
        &::after {
          content: '';

          position: absolute;
          top: calc(100% - .5em);
          left: 1em;

          display: block;
          height: .3rem;
          width: calc(100% - 2em);

          background-color: var(--yellow-500);
        }
      }
    }
  }

  &__search {
    padding-right: 7rem;
    padding-left: 4.2rem;

    font-weight: 400;

    svg {
      left: 1rem;
    }
  }

  .algolia-search {
    position: absolute;
    left: 0;
    top: 0;
    z-index: 999;

    display: flex;
    align-items: flex-start;
    justify-content: center;
    height: 100vh;
    width: 100%;
    padding: 2.4rem;

    // background-color: rgba(255,255,255,.8);
    background-color: hsla(170, 29%, 75%, .6);
  }
}
</style>