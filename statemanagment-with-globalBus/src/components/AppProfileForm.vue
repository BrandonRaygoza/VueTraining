<template>
  <section class="md:w-2/3 flex flex-col p-12 items-center">
    <!-- Inputs -->
    <div class="flex flex-col">
      <label class="flex text-gray-800 mb-2" for="name">Name</label>
      <input
        id="name"
        type="text"
        name="name"
        v-model="name"
        class="border-2 border-solid border-blue-200 rounded px-2 py-1"
      />
    </div>
    <div class="flex flex-col mt-2">
      <label class="flex text-gray-800 mb-2" for="occupation">Occupation</label>
      <input
        id="occupation"
        type="text"
        name="occupation"
        v-model="occupation"
        class="border-2 border-solid border-blue-200 rounded px-2 py-1"
      />
    </div>
    <div class="flex flex-row mt-12">
      <button type="submit" @click="submitForm()">Submit</button>
    </div>
  </section>
</template>
<script>
import eventBus from '../event-bus'

export default {

  data() {
    return {
      name: '',
      occupation: '',
    }
  },

  /*the name of the event to subscribe to (as a string) and a callback to which the event will be passed through a publish operation. */
  mounted(){
    eventBus.$on('profileUpdate',this.update)
  },

  /*$off, the unsubscribe operation, needs to be called with the same parameters with which the subscribe operation was called.*/
  beforeDestroy(){
    eventBus.$off('profileUpdate',this.update)
  },

  methods: {

    /*. $emit(eventName, payload) is the event bus' publish operation. $emit supports two parameters— the name of the event (as a string) and a payload, which is optional and can be any object. */
    submitForm() {
      eventBus.$emit('profileUpdate', {
        name: this.name,
        occupation : this.occupation
      })
    }, 

    update(formData){
      this.name = formData.name || ''
      this.occupation = formData.occupation || ''
    }
  }
}
</script>
