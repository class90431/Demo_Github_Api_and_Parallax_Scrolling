<template>
	<div
		class="bg-halley"
		ref="bg"
	>
		<div class=" mx-auto px-4 sm:px-8">
			<div class="py-8">
				<div>
					<h2 class="text-2xl font-semibold leading-tight">Zack's Repositories</h2>
				</div>
				<div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
					<div class="inline-block min-w-full shadow rounded-lg overflow-hidden">
						<table class="min-w-full leading-normal">
							<thead>
								<tr class="bg-gray-100 bg-opacity-75">
									<th class="px-5 py-3 border-b-2 border-gray-200 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">
										Title
									</th>
									<th class="px-5 py-3 border-b-2 border-gray-200 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">
										description
									</th>
									<th class="px-5 py-3 border-b-2 border-gray-200 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">
										url
									</th>
									<th class="px-5 py-3 border-b-2 border-gray-200 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">
										create
									</th>
								</tr>
							</thead>
							<tbody>
								<tr
									v-for="(item, index) in data"
									:key="index"
								>
									<td class="px-5 py-5 border-b border-gray-200 bg-opacity-20 bg-white text-sm">
										<div class="flex items-center">
											<div class="ml-3">
												<a
													:href="item.html_url"
													target="_blank"
													class="text-blue-900 whitespace-no-wrap text-left"
												>
													{{ item.name }}
												</a>
											</div>
										</div>
									</td>
									<td class="px-5 py-5 border-b border-gray-200 bg-opacity-20 bg-white text-sm w-3">
										<p class="text-gray-900 whitespace-no-wrap text-center">{{ item.description }}</p>
									</td>
									<td class="px-5 py-5 border-b border-gray-200 bg-opacity-20 bg-white text-sm">
										<p class="text-gray-900 whitespace-no-wrap text-left">
											{{ item.html_url }}
										</p>
									</td>
									<td class="px-5 py-5 border-b border-gray-200 bg-opacity-20 bg-white text-sm">
										<p class="text-gray-900 whitespace-no-wrap text-left">
											{{ item.created_at }}
										</p>
									</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'App',
	data() {
		return {
			data: null,
			scrollTop: 0,
		}
	},
	created() {
		this.getRepositoryData()
	},
	mounted() {
		window.addEventListener('scroll', this.handleScroll, true)
	},
	methods: {
		getRepositoryData() {
			fetch('https://api.github.com/users/class90431/repos')
				.then((response) => response.json())
				.then((data) => {
					// console.log(data)
					this.data = data
				})
				.catch((error) => {
					console.log(error)
				})
		},
		handleScroll() {
			let scrollTop = document.documentElement.scrollTop
			this.scrollTop = scrollTop
			this.$refs.bg.style['background-position-x'] = this.scrollTop + '%'
		},
	},
}
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
.bg-halley {
	background-image: url('./assets/halley.jpg');
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center center;
}
</style>
