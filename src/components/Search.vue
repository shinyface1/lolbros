<!--diable CORS use this in cmd: 
  1. cd C:\Program Files (x86)\Google\Chrome\Application
  2. chrome.exe --disable-web-security --user-data-dir=/users/ross/lol-search
-->
<template>
  <div class="search">
    <h2>Type in Username</h2>
    <form v-on:submit.prevent="getResult(summonerName, apiKey)">
      <input type="text" placeholder="Username" v-model="summonerName" />
    </form>
    <p v-if="errors.length">
        <b>Please correct the following error(s):</b>
   
      </p>   
    <div v-if="summonerResults">
        <p>Summoner Name: {{summonerResults.name}}</p>
        <p>Summoner Level: {{summonerResults.summonerLevel}}</p>
        <p>Profile Icon ID: {{summonerResults.profileIconId}}</p>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: 'search',
  data () {
    return {
      apiKey: 'RGAPI-0393717b-8be1-4618-9d6a-8017f075e0b3',
      errors: [],
      summonerName: '',
      summonerResults: ''
    }
  },
  methods: {
    getResult(summonerName, apiKey) {
      axios.get('https://euw1.api.riotgames.com/lol/summoner/v4/summoners/by-name/' + summonerName + '?api_key=' + apiKey).then(response => {
          window.console.log(response.data);
          window.console.log(apiKey);
          this.summonerResults = response.data;
        })
        this.errors = [];
        if (!this.summonerName) {
          this.errors.push('Username required.');
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
