<template>
  <div id="app">
    <input type="text" v-model="id" />
    <!-- <button @click="getTeam()">Search</button> -->

    <div v-if="this.id != ''">
       <InfoEquipo v-bind:idTeam="this.id"/>
    </div>
   
  </div>
</template>

<script>
import InfoEquipo from './components/InfoEquipo.vue'

export default {
  name: 'App',
  data(){
    return{
      id: "",
    }
  },

  components: {
    InfoEquipo,
  }
}
</script>


