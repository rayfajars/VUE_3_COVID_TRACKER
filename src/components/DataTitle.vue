<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10">
      <!-- {{ date }} -->
      {{timestamp}}
    </div>
  </div>
</template>

<script>

import moment from 'moment'



export default {
  name: "DataTitle",
  props: ["text", "date"],
  computed:{
    // membuat object/variable yg baru
    timestamp:function(){
        return moment(this.date).format('DD MMMM YYYY HH:mm')
    }
  }
};
</script>

<style></style>
