<template>
  <main v-if="!loading" class="min-h-[75vh]">
    <DataTitle :text="title" :dataDate="dataDate" />

    <CountrySelect :countries="countries" @get-country="getCountryData" />

    <DataBoxes :stats="stats" />
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "HomeView",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      return await res.json();
      // return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    // console.log(data);
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
