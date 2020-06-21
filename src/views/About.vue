<template>
  <div class="about">
    <h1>This is an Video details page</h1>
    <video width="450" controls :src="id" :poster="poster"></video>
  </div>
</template>

<script>
export default {
  name: "Details",
  data() {
    return {
      details: null,
      id: this.$route.params.id,
      poster: this.$route.query.poster,
      videos: [],
    };
  },
  created() {},
  methods: {},
};
</script>
