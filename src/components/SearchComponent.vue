<template>
  <ClientOnly>
    <ais-instant-search
      :search-client="searchClient"
      index-name="dev_reliably_docs"
      v-click-outside="close"
    >
      <ais-configure
        :hits-per-page.camel="10"
        :distinct="true"
      />
      <ais-search-box
        placeholder="Search"
        :show-loading-indicator="true"
        autofocus
        ref="search"
      ></ais-search-box>
      <ais-state-results>
        <template
          v-slot="{ state: { query }, results: { hits } }"
        >
          <div class="search-results--empty" v-if="query.length > 0 && !hits.length">
            <p>No results found for your query: <strong>{{ query }}</strong></p>
          </div> 
          <ais-hits v-else-if="query.length > 0 && hits.length">
            <div class="search-results" slot-scope="{ items }">
              <div class="search-results__list">
                <template v-for="item in items">
                  <g-link
                    :to="item.path"
                    @click.native="close"
                    class="search-card"
                  >
                    <span class="search-card__category">{{item.categories[0]}}</span>
                    <span class="search-card__title">{{item.title}}</span>
                    <p class="search-card__excerpt">{{ item.excerpt }}</p>
                  </g-link>
                </template>
              </div>
              <ais-pagination />
            </div>
          </ais-hits>
          <div v-else></div>
        </template>
      </ais-state-results>
      
      <ais-powered-by />
    </ais-instant-search>
  </ClientOnly>
</template>

<script>
import algoliasearch from 'algoliasearch/lite'

function onCatch(err) {
  console.warn(err)
}

export default {
  components: {
    AisInstantSearch: () =>
      import ('vue-instantsearch')
      .then(a => a.AisInstantSearch)
      .catch(onCatch),
    AisConfigure: () =>
      import ('vue-instantsearch')
      .then(a => a.AisConfigure)
      .catch(onCatch),
    AisSearchBox: () =>
      import ('vue-instantsearch')
      .then(a => a.AisSearchBox)
      .catch(onCatch),
    AisStateResults: () =>
      import ('vue-instantsearch')
      .then(a => a.AisStateResults)
      .catch(onCatch),
    AisHits: () =>
      import ('vue-instantsearch')
      .then(a => a.AisHits)
      .catch(onCatch),
    AisPagination: () =>
      import ('vue-instantsearch')
      .then(a => a.AisPagination)
      .catch(onCatch),
    AisPoweredBy: () =>
      import ('vue-instantsearch')
      .then(a => a.AisPoweredBy)
      .catch(onCatch)
  },
  data() {
    return {
      searchClient: algoliasearch(
        process.env.GRIDSOME_ALGOLIA_APP_ID,
        process.env.GRIDSOME_ALGOLIA_ADMIN_KEY
      ),
    };
  },
  methods: {
    close() {
      this.$emit('close-search');
    }
  },
}
</script>

<style lang="scss">
.ais-InstantSearch {
  width: 100%;
  max-width: 70rem;
  overflow: hidden;

  border-radius: 1rem;
  box-shadow: 0 .6rem 2.4rem var(--blue-300);
  box-shadow: 0 .6rem 2rem rgba(0,0,0,.2);
}

.ais-SearchBox {
  display: flex;
  justify-content: center;

  &-form {
    position: relative;

    width: 100%;
  }

  &-input {
    height: 6rem;
    width: 100%;
    padding: 1rem 1.6rem 1rem 6rem;

    border: none;
    -webkit-appearance: textfield;
    -webkit-appearance: none;

    color: var(--blue-600);
    font-size: 2.4rem;
    font-weight: 300;
    line-height: 1;

    &:focus {
      outline: none;
    }

    &::-webkit-search-decoration,
    &::-webkit-search-cancel-button,
    &::-webkit-search-results-button,
    &::-webkit-search-results-decoration {
      -webkit-appearance: none;
    }

  }

  &-submit {
    position: absolute;
    top: 0;
    left: 0;

    display: flex;
    align-items: center;
    justify-content: center;
    height: 6rem;
    width: 6rem;
    padding: 0;

    background-color: transparent;
    border: none;
    cursor: pointer;

    svg {
      margin-top: .3rem;
      height: 2rem;
      width: 2rem;

      fill: var(--blue-500);
    }
  }

  &-reset {
    position: absolute;
    top: 2.3rem;
    left: calc(100% - 4rem);

    height: 1.4rem;
    width: 1.4rem;
    padding: 0;

    background-color: transparent;
    border: none;
    cursor: pointer;

    svg {
      height: 100%;
      width: 100%;
      fill: var(--blue-300);
    }


  }
}

.ais-StateResults {
  max-height: calc(100vh - 13rem);

  background-color: white;
  border-top: .1rem solid var(--blue-200);

  .search-results {
    position: relative;
    
    &--empty {
      padding: 1.5rem;

      p {
        margin: 0;
      }
    }

    &__list {
      max-height: calc(100vh - 20rem);
      overflow-y: auto;
    }
  }
}

.ais-Hits {
  width: 100%;
  max-width: 90rem;

  .search-card {
    display: block;
    padding: .75rem 1.5rem;

    border-top: .1rem solid var(--blue-200);

    text-decoration: none;

    &:hover {
      background-color: var(--blue-200);
    }

    &__category {
      display: block;
      
      // color: var(--blue-500);
      color: var(--yellow-600);
      font-size: 1rem;
      text-transform: uppercase;
    }

    &__title {
      color: var(--blue-700);
      font-size: 1.6rem;
    }

    &__excerpt {
      margin: 0;

      color: var(--blue-600);
      font-size: 1.4rem;
    }
  }
}

.ais-Pagination {
  &-list {
    display: flex;
    justify-content: center;
    margin: 0;
    padding: 1.5rem;

    border-top: .1rem solid var(--blue-200);
    list-style-type: none;

    > * + * {
      margin-left: 1.2rem;
    }
  }

  &-item {
    height: 2.4rem;
    width: 2rem;

    border-radius: .5rem;

    color: var(--blue-600);
    text-align: center;

    &--disabled {
      opacity: .5;
    }

    &--selected {
      background-color: var(--blue-600);

      color: white;
    }

    &:hover:not(.ais-Pagination-item--disabled):not(.ais-Pagination-item--selected) {
      background-color: var(--blue-200);
    }
  }

  &-link {
    display: block;
    height: 100%;
    width: 100%;

    color: inherit;
    text-decoration: none;
  }
}

.ais-PoweredBy {
  display: none;
}
</style>