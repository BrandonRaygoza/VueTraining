<template>
  <section class="md:w-1/3 flex flex-col p-12">
  <!-- Profile Card -->
    <h3 class="font-bold font-lg">{{ formData.name }}</h3>
    <p class="mt-2">{{ formData.occupation }}</p>
  </section>
</template>

<script>
import eventBus from '../event-bus'
export default {
  // props: {   Ya no es necesario porque ya no vienen de otro componente (del padre especificamente, que era el que funcionaba como puente, entre el componente origen y destino)
  //   formData: {
  //     type: Object,
  //     default() {
  //       return {}
  //     }
  //   }
  // },

  data(){
    return{
      formData : {}
    };
  },

  methods:{
    update(formData){
      this.formData = formData
    }
  },

  /*the name of the event to subscribe to (as a string) and a callback to which the event will be passed through a publish operation. */
  mounted(){
    eventBus.$on('profileUpdate',this.update)
  },

  /*$off, the unsubscribe operation, needs to be called with the same parameters with which the subscribe operation was called.*/
  beforeDestroy(){
    eventBus.$off('profileUpdate',this.update)
  }

  
}
</script>
