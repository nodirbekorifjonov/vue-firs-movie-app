<template>
  <div class="btn-group">
    <PrimaryButton
      v-for="btn in filterButtons"
      :key="btn.name"
      type="button"
      @click="filterHandler(btn.name)"
      :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark']"
    >
      {{ btn.title }}
    </PrimaryButton>
  </div>
</template>
<script>
export default {
  data() {
    return {
      filterButtons: [
        { title: "Barcha kinolar", name: "all" },
        { title: "Mashhur kinolar", name: "popular" },
        { title: "Eng ko'p ko'rilgan kinolar", name: "mostViewers" },
      ],
      filter: "all",
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilterHandler(this.filter);
    },
  },
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
};
</script>
<style scoped></style>
