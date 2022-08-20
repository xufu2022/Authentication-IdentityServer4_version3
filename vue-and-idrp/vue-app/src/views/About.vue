<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div v-for="(item,index) in values" :key="index">
      <p>{{item}}</p>
    </div>
    <button @click="callApi">Call API</button>
    <button @click="callSecureApi">Call Secure API</button>
    <div v-for="service in services" :key="service.iconUri">
      <p>
        <img :src="service.iconUri" />
        <a :href="service.uri">{{service.name}}</a>
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      values: ["no data yet"],
      services: []
    }
  },
  methods: {
    async callApi() {
      try {
        const response = await axios.get("https://localhost:44326/api/values");
        this.values = response.data;
      } catch (err) {
        this.values.push("Ooops!" + err);
      }
    },
    async callSecureApi() {
      try {
        const response = await axios.get("https://localhost:44326/api/services");
        this.services = response.data;
      } catch (err) {
      debugger;
        console.log('secure api call failed');
      }
    }
  }
}
</script>

