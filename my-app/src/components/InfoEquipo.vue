<template>
  <div>
    <!-- <input type="text" v-model="id" />
    <button @click="getTeam()">Search</button> -->

    Id:
    <p>{{ idTeam }}</p>
    <p></p>
    <div v-if="team != null" class="info">
      <ul>
        <li>
          <h3>Team: {{ team.strTeam }}</h3>
          <ul>
            <li>Team short: {{ team.strTeamShort }}</li>
            <li>Formed year: {{ team.intFormedYear }}</li>
            <li>Sport: {{ team.strSport }}</li>
            <li>League: {{ team.strLeague }}</li>
          </ul>
        </li>
      </ul>
    </div>
    <h1 v-else>No results</h1>
  </div>
</template>

<script>
import axios from "axios";
const url = "https://www.thesportsdb.com/api/v1/json/1/lookup_all_teams.php";

export default {
  //props: ["idTeam"],
    props: {
      idTeam: {
          type: String,
          required: true
      },
    },

  data() {
    return {
      //id: "",
      responseTeam: null,
    };
  },

  watch: {
    idTeam: async function(newValue, oldValue) {
      console.log(`Was: ${oldValue}, now: ${newValue}`);
      this.idTeam = newValue;
      await this.getTeam();
    },
  },

  methods: {
    async getTeam() {
      return axios.get(`${url}?id=${this.idTeam}`).then((response) => {
        console.log(`Response data: ${JSON.stringify(response.data)}`);
        this.responseTeam = response.data.teams[0];
      });
    },
  },

  computed: {
    team() {
      return this.responseTeam ? this.responseTeam : null;
    },
  },
};
</script>

<style></style>
