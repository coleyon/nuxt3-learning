<template>
  <v-main>
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md4>
          <v-card class="elevation-12">
            <v-toolbar dark color="primary">
              <v-toolbar-title>Login</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-form>
                <v-text-field
                  v-model="username"
                  id="username"
                  :rules="userNameRules"
                  :counter="128"
                  label="UserID"
                  prepend-icon="mdi-id-card"
                  type="text"
                  required
                ></v-text-field>
                <v-text-field
                  v-model="password"
                  id="password"
                  :rules="passwdRules"
                  :counter="64"
                  prepend-icon="mdi-key"
                  label="Password"
                  type="password"
                  required
                ></v-text-field>
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn type="submit" color="primary" @click="submitLogin">
                Login
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </v-main>
</template>

<script>
export default {
  layout: 'login',
  data() {
    return {
      username: '',
      password: '',
      userNameRules: [
        (v) => !!v || 'username is required',
        (v) => /.+@.+/.test(v) || 'username must be email format',
      ],
      passwdRules: [
        (v) => !!v || 'passworwd is required',
        (v) => v.length >= 6 || 'password must be more than 6 characters',
      ],
    };
  },

  methods: {
    async submitLogin() {
      // post the auth request to the backend api
      try {
        // generate request payloads as a url encodd form input.
        const urlEncodedFormInput = new URLSearchParams();
        urlEncodedFormInput.append('username', this.username);
        urlEncodedFormInput.append('password', this.password);
        // logging in
        await this.$auth.loginWith('local', {
          data: urlEncodedFormInput,
        });
        // get account info
        const result = await this.$axios.get('/users/me');
        console.debug('Responsed token is:', result.data);
        await this.$auth.setUser(result.data.email);
        // // example: how to logout
        // console.debug('loggedin? ', this.$auth.loggedIn);
        // console.debug('logging out.... ');
        // await this.$auth.logout();
        // console.debug('loggedin? ', this.$auth.loggedIn);
        this.flashMessage.success({ title: 'Logged in.' });
        this.$router.push('/');
      } catch (err) {
        console.error(err);
        this.flashMessage.warning({
          title: 'Login Failed',
          message: 'Invalid ID or Password.',
        });
      }
    },
  },
};
</script>

<style scoped></style>
