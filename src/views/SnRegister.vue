<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign up</h1>
          <p class="text-xs-center">
            <router-link :to="{name: 'login'}">Already have an account?</router-link>
          </p>
          <SnValidationErrors v-if="$store.getters.validationErrors"
                              :validationErrors="$store.getters.validationErrors"/>
          <form @submit.prevent="onSubmit">
            <fieldset class="form-group">
              <input
                  class="form-control form-control-lg"
                  type="text"
                  placeholder="Username"
                  v-model="username"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                  class="form-control form-control-lg"
                  type="text"
                  placeholder="Email"
                  v-model="email"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                  class="form-control form-control-lg"
                  type="password"
                  placeholder="Password"
                  v-model="password"
              />
            </fieldset>
            <button class="btn btn-lg btn-primary pull-xs-right" :disabled="$store.getters.isSubmitting">
              Sign Up
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SnValidationErrors from '@/components/SnValidationErrors';
import {actionTypes} from '@/store/modules/auth';

export default {
  name: 'SnRegister',
  components: {
    SnValidationErrors,
  },
  data() {
    return {
      email: '',
      password: '',
      username: '',
    };
  },
  computed: {},
  methods: {
    onSubmit() {
      this.$store.dispatch(actionTypes.register, {
        email: this.email,
        password: this.password,
        username: this.username,
      }).then((user) => {
        console.log('successfully register user', user);
        this.$router.push({name: 'login'});
      });
    },
  },
};
</script>
