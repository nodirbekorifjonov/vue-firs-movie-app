<template>
  <Box class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent="addMovie">
      <Input
        class="new-movie-label"
        placeholder="Qanday kino?"
        v-model="name"
      />
      <Input
        type="number"
        class="new-movie-label"
        placeholder="Nechi marotaba ko'rilgan?"
        v-model="viewers"
      />

      <PrimaryButton type="submit" class="btn-outline-dark"
        >Qo'shish</PrimaryButton
      >
    </form>
  </Box>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  data() {
    return {
      name: "",
      viewers: "",
    };
  },
  methods: {
    addMovie() {
      if (!this.name || !this.viewers) return;
      const newMovie = {
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false,
      };

      this.$emit("createMovie", newMovie);
      this.name = "";
      this.viewers = "";
    },
  },
};
</script>

<style scoped>
.movie-add-form {
  margin-top: 2rem;
}
</style>
