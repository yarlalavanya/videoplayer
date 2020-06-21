<template>
  <div class="home">
    <div class="container">
      <slider ref="slider" :options="options">
        <!-- slideritem wrapped package with the components you need -->
        <slideritem v-for="(item, index) in videos" :key="index" :style="style">
          <router-link
            :key="index"
            :to="{
              name: 'Details',
              params: { id: item.video },
              query: { poster: item.poster },
            }"
          >
            <img :src="item.poster" />
            <div>{{ item.title }}</div>
          </router-link>
        </slideritem>
        <!-- Customizable loading -->
        <div slot="loading">loading...</div>
      </slider>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { slider, slideritem } from "vue-concise-slider";

export default {
  data() {
    return {
      loading: false,
      videos: null,
      name: "kranti",
      settings: {
        dots: true,
        focusOnSelect: true,
        infinite: true,
        speed: 500,
        slidesToShow: 3,
        slidesToScroll: 3,
        touchThreshold: 5,
      },
      options: {
        currentPage: 0,
        infinite: 4,
        slidesToScroll: 4,
        loop: true,
      },
      style: {
        background: "#7caabe",
        width: "23.5%",
        "margin-right": "2%",
      },
    };
  },
  name: "Home",
  beforeMount() {
    this.getData();
  },

  methods: {
    async getData() {
      const res = await fetch("http://hybridtv.ss7.tv/techtest/movies.json");
      const data = await res.json();

      this.videos = data.data;
      console.log(this.videos);
    },
    goTodetail(id) {
      this.$router.push({ name: "details/" + id });
    },
  },
  components: { slider, slideritem },
};
</script>
