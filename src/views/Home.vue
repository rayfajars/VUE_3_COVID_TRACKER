<template>
  <main v-if="loading">
    <DataTitle :text="title" :date="date"></DataTitle>
    <DataBoxes :stats="stats"></DataBoxes>
    <CountrySelect
      @get-country="getCountryData"
      :countries="countries"
    ></CountrySelect>

    <button @click="clearCountryData" v-if="stats.Country" class="bg-blue-700 text-white rounded p-3 mt-10 focus:outline-non hover:bg-blue-600">
      Clear Country
    </button>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-blue-700 text-5xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-25 m-auto" alt="" />
  </main>
</template>

<script>
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import CountrySelect from "../components/CountrySelect.vue";
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: false,
      title: "Global",
      date: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/loading.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      console.log(country);
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData(){
      this.loading = false;
      const data = await this.fetchCovidData()
      this.title = "Global"
      this.stats = data.Global;
      this.loading = true
      // console.log(data)
    }
  },

  async created() {
    const data = await this.fetchCovidData();

    // console.log(data);
    // console.log(data.Date);
    this.date = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = true;
  },
};
</script>
