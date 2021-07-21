<template>
  <article class="tabs-container">
    <header class="tabs">
      <ul>
        <li v-for="(tab, index) in tabs" :key="index">
          <div class="nav-item"
              :class="{ 'is-active': tab.isActive }"
              @click="selectTab(tab)">
            {{ tab.name }}
          </div>
        </li>
      </ul>
    </header>
    <section class="tabs-detail">
      <slot></slot>
    </section>
  </article>
</template>

<script>
  export default {
    data: () => {
      return {
        tabs: []
      }
    },
    methods: {
      selectTab(selectedTab) {
        this.tabs.forEach(tab => {
          tab.isActive = tab.name === selectedTab.name;
        });
      }
    },
    created() {
      this.tabs = this.$children;
    }
  }
</script>

<style lang="scss">
.tabs-container {
  margin-top: 4rem;

  .tabs {
    margin: 0 10px;
    
    font-weight: bold;

    ul {
      display: flex;
      padding: 0;

      list-style: none;
      li {
        margin-right: 40px;
      }
      .nav-item {
        position: relative;

        cursor: pointer;

        &:before {
          content: "";

          position: absolute;
          top: calc(100% + .3rem);
          left: 0;

          display: block;
          height: .3rem;
          width: 100%;

          background-color: transparent;
        }

        &:hover {
          &::before {
            background-color: var(--yellow-500);
          }
        }
        &.is-active {
          &::before {
            background-color: var(--body-color);
          }
        }
      }
    }
  }
  .tabs-detail {
    padding: 1.6rem;

    background-color: var(--blue-200);
    border-radius: 5px;
  }
}
</style>