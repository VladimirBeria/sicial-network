<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign in</h1>
          <p class="text-xs-center">
            <router-link :to="{name: 'register'}">Need an account?</router-link>
          </p>
          <SnValidationErrors v-if="$store.getters.validationErrors"
                              :validationErrors="$store.getters.validationErrors"/>
          <form @submit.prevent="onSubmit">
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
              Sign In
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
  name: 'SnLogin',
  components: {
    SnValidationErrors
  },
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    onSubmit() {
      this.$store.dispatch(actionTypes.login, {
        email: this.email,
        password: this.password,
      }).then(() => {
        console.log('successfully logged user');
        this.$router.push({name: 'home'});
      });
    },
  }
};
</script>

<style scoped>

</style>