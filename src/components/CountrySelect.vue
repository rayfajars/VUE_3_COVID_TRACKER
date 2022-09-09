<template>
  <!-- {{countries}} -->
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select block w-full border p-3 rounded mt-10"
  >
    <option value="0" selected="true" disabled="disabled">
      Select Country
    </option>
    <option v-for="country in countries" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      //   console.log();
      //   const selected = event.target.value;
      const country = this.countries.find((item) => item.ID === this.selected);
      // console.log(country)
      this.$emit("get-country", country);
    },
  },
};
</script>

<style></style>
