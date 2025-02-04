<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter((c) => c.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>
      <MovieList
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
      />
      <MovieAdd @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import MovieAdd from "../movie-add/MovieAdd.vue";
import MovieList from "../movie-list/MovieList.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import AppInfo from "../app-info/AppInfo.vue";
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAdd,
  },
  data() {
    return {
      movies: [
        {
          name: "Omar",
          viewers: 811,
          favourite: false,
          like: true,
          id: 1,
        },
        {
          name: "Empire of Osman",
          viewers: 411,
          favourite: true,
          like: false,
          id: 2,
        },
        {
          name: "Ertugrul",
          viewers: 711,
          favourite: false,
          like: false,
          id: 3,
        },
      ],
      term: "",
      filter: "all",
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        } else {
          return item;
        }
      });
    },
    onDeleteHandler(id) {
      this.movies = this.movies.filter((c) => c.id !== id);
    },
    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr;
      }
      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1);
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 500);
        default:
          return arr;
      }
    },
    updateTermHandler(term) {
      this.term = term;
    },
    updateFilterHandler(filter) {
      this.filter = filter;
    },
  },
};
</script>

<style>
.app {
  height: 100vh;
  color: black;
}

.content {
  width: 1000px;
  min-height: 700px;
  background: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
