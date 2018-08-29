<template>
	<b-container>
		<b-row>
			<b-col class="mx-auto mt-5 mb-3" md="8" sm="12" v-for="(repo, index) in repos" :key="index">
				<div class="repository bg-light p-5 shadow rounded">
					<b-row>
						<b-col md="2" sm="6" class="pl-2  repo-img">
							<i class="fas fa-code-branch fa-3x"></i>
						</b-col>
						<b-col md="8" sm="6" class="text-center repo-info">
							<h4 class="repo-name">{{repo.name}}</h4>
							<small class="my-2 d-block">{{repo.description}}</small>
							  <b-button-group>
									<b-button variant="light">
										<i class="fas fa-code-branch"></i>
										Forks {{repo.forks}}
									</b-button>
									<b-button variant="light">
										<i class="fas fa-star"></i>
										Stars {{repo.stargazers_count}}
									</b-button>
									<b-button variant="light" @click="showRepo(repo.name, repo.owner.login)">
										<i class="fas fa-users"></i>
										Show Contributors
									</b-button>
								</b-button-group>
						</b-col>
					</b-row>
				</div>
			</b-col>
		</b-row>
	</b-container>
</template>
<script>
import config from '../../config/config.js'
import axios from 'axios'
export default {
props: ['repos'],
	data() {
		return {
			isFalse: false
		}
	},
	methods : {
		showRepo (repoName,ownerName) {
			let self = this
			axios.get(`https://api.github.com/repos/${ownerName}/${repoName}/stats/contributors`, config)
			.then((response)=> console.log (response.data.length))
		}
	}
}
</script>
<style scoped>
</style>
