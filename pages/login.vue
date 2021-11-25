<template>
  <v-row justify="center" align="center">
    <v-col class="text-center">
      <form @submit.prevent>
        <h1>Login</h1>
        <label for="username" class="text-left">Username</label>
        <input v-model="user.username" id="username" type="text" />
        <label for="password" class="text-left">Password</label>
        <input v-model="user.password" id="password" type="password" />
        <v-btn color="primary" nuxt to="/api/v1/login/access-token">
          Login
        </v-btn>
        <v-spacer />
      </form>
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: 'login',
  data() {
    return {
      user: {
        username: '',
        password: '',
      },
    };
  },

  // check loggedin
  methods: {
    loginUser() {
      this.$auth.loginWith('local', {
        data: this.user,
      });
    },
  },

  // methods: {
  //   async login() {
  //     try {
  //       await this.$auth.loginWith('local', {
  //         data: {
  //           auth: {
  //             username: this.username,
  //             password: this.password,
  //           },
  //         },
  //       });
  //       if (!this.$auth.loggedIn) {
  //         throw Error('You Must Login.');
  //       }
  //       this.$router.push('/');
  //     } catch (e) {
  //       alert(`Login Failed.`);
  //     }
  //   },
  // },
};
</script>

<style scoped>
div {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  font-size: 14px;
  margin: 0 0.5rem;
  margin-bottom: 0.25rem;
}

input {
  font-size: 16px;
  padding: 0.75rem 1rem;
  margin: 0 0.5rem;
  margin-bottom: 0.5rem;
  border: 1px solid #dedede;
  border-radius: 0.5rem;
  box-shadow: none;
  box-sizing: border-box;
}

.button {
  margin-top: 0.5rem;
}

.button[disabled] {
  cursor: default;
  opacity: 0.5;
  cursor: not-allowed;
}
.button {
  background: var(--primary-color);
  padding: 0.75rem 1.5rem;
  outline: none;
  border-radius: 0.5rem;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  color: white;
  font-weight: 500;
  text-transform: uppercase;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  letter-spacing: 0.5px;
  margin: 0 0.5rem;
}

button:hover {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  opacity: 0.8;
}
</style>
