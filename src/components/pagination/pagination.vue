<template>
  <Box class="d-flex justify-content-center">
    <nav aria-label="pagination">
      <ul class="pagination">
        <li
          class="page-item"
          :class="page == 1 && 'disabled'"
          @click="previousPage"
        >
          <span class="page-link">Previous</span>
        </li>
        <li
          v-for="pageNumber in totalPages"
          :key="pageNumber"
          :class="{ active: page == pageNumber }"
          @click="changePage(pageNumber)"
        >
          <span class="page-link">{{ pageNumber }}</span>
        </li>
        <li
          class="page-item"
          :class="page >= totalPages && 'disabled'"
          @click="nextPage"
        >
          <span class="page-link" href="#">Next</span>
        </li>
      </ul>
    </nav>
  </Box>
</template>
<script>
export default {
  data() {
    return {
      myPage: 1,
    };
  },
  props: {
    totalPages: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    },
  },
  methods: {
    nextPage() {
      if (this.myPage < this.totalPages) {
        this.$emit("nextPage", (this.myPage += 1));
      }
    },
    previousPage() {
      if (this.myPage > 1) {
        this.$emit("previousPage", (this.myPage -= 1));
      }
    },
    changePage(pageNumber) {
      this.$emit("changePage", (this.myPage = pageNumber));
    },
  },
};
</script>
<style scoped>
.pagination {
  user-select: none;
  cursor: pointer;
}
</style>
