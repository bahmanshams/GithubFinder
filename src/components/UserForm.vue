<template>
  <div>
    <b-container>
      <b-row>
        <b-col class="mx-auto mt-5" md="6" sm="12">
          <div class="user-form-container py-5 px-3 rounded shadow-sm bg-light">
            <h4 class="text-center my-3 text-muted">Get Your Github Account's Info</h4>
            <form class="user-form__inner" @submit.prevent="handleSubmit">
              <b-form-group id="username" :label-cols="4" breakpoint="md" label="Github Username" label-for="usernameInput">
                <b-form-input id="usernameInput" @keyup="handleSubmit" v-model="username" placeholder="Enter Your Github Username"></b-form-input>
              </b-form-group>
              <b-button type="submit" variant="primary" class="shadow" :disabled="isLoading" block>
                <i v-if="!isLoading" class="fas fa-search"></i>
                <i v-if="isLoading" class="fas fa-spinner fa-lg fa-spin"></i>
                Get Your Info
              </b-button>
            </form>
          </div>
        </b-col>
      </b-row>
    </b-container>
    <user-repos :repos="userRepo"/>
  </div>
</template>
<script>
import config from '../../config/config.js'
import axios from 'axios'
import UserRepos from './UserRepos.vue'
export default {
	data() {
		return {
      username: '',
			isLoading: false,
      userRepo: {}
		}
	},
  components: {
    UserRepos
  },
	methods: {
		handleSubmit() {
      let self = this
			this.isLoading= !this.isLoading
			axios.get(`https://api.github.com/users/${this.username}/repos`, config)
        .then(function (repos){
          self.userRepo = repos.data
          self.isLoading = !self.isLoading
        })
        .catch(function (err){
          console.log(err)
          self.userInfo = ''
          self.isLoading = !self.isLoading
        })
		}
	}
}
</script>

<style scoped>
.user-form-container{
	font-family: 'Francois One', sans-serif;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
*:not(i){
  font-family: 'Francois One', sans-serif;
}
</style>
