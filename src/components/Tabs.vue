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

<style lang="scss" scoped>
.tabs-container {
    padding: 0.25rem 1rem;
    background-color: var(--blue-100);
    border-radius: 5px;
    margin-top: 4rem;
}
  .tabs {
    margin: 0 10px;
     border-bottom: 2px solid white;
     font-weight: bold;
  }
  .tabs-detail {
    margin-top: -30px;
    padding: 1rem 1.5rem 0.5rem;
  }
  ul {
    display: flex;
    padding: 0;
    list-style: none;
    li {
      margin-right: 40px;
    }
    .nav-item {
      cursor: pointer;
      &:hover {
        color: var(--yellow-500);
      }
      &.is-active {
        color: var(--yellow-500)
      }
    }
  }
</style>