<template>
  <div class="home">
    Hello Home
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld
  },methods:{
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data;
    }
  },  
  async created(){
    const data = await this.fetchCovidData()

    console.log(data)
  }
}
</script>
