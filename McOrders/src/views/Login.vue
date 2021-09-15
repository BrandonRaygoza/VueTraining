<template>
  <div class="about">
    <h1>Login</h1>
    <div>
      <label>Username</label><br>
      <input type="text" placeholder="e.g., juanito" v-model="user.username" /><br><br>
      <label>Password</label><br>
      <input type="password" placeholder="e.g., mypassword" v-model="user.password" /><br><br>
      <button @click="login">Login</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
        nombre: "",
        user:{
            username: "",
            password: ""
        },

      userdata: {
        username: "brandon",
        password: "1234",
      },
    };
  },

  methods: {
    login: function() {
      if(this.user.username !== this.userdata.username || this.user.password !== this.userdata.password){
          alert("Credenciales invalidas")
          return;
      }

      this.$router.push({
          name: 'GenerateOrder',
          params: {username: this.user.username}
      });
    },
  },
};
</script>
