<template>
  <div class="login">
    <h3>Login</h3>
    <form class="login__form" @submit="checkForm">
      <input v-model="user.email" type="email" placeholder="Email" />
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import * as config from "../../../config";

export default {
  name: "adminLogin",
  data: function() {
    return {
      errors: [],
      user: {}
    };
  },
  methods: {
    checkForm: function(evt) {
      evt.preventDefault();

      this.errors = [];

    //   if (this.honeyName) {
    //     this.errors.push("Sooooooooooonnkk!");
    //   }
      if (!this.user.email) {
        this.errors.push("Email required");
      }
      if (!this.errors.length) {
        this.userLogin();
      }
    },
    userLogin: function() {
      return axios
        .post(`${config.apiUrl}/users/login`, this.user)
        .then(response => {
          let user = response.data.user;
          if (user) {
            localStorage.userEmail = user.email;
            this.$router.push({ name: "adminProfile", params: {user: user.id}});
          } else {
            // SOMETHING ELSE
          }

          // console.log('user', response.data.user);
          //   this.$router.push({ path: "/" });
        })
        .catch(function(error) {
          // handle error
          console.log(error);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.login {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  &__form {
    display: flex;
    flex-direction: column;
    input {
      margin-bottom: 5px;
    }
  }
}
</style>