<script>
	export let name;
	import Titlebar from "./components/titlebar.svelte"
	import Item from "./components/item.svelte"
	import Youtube from "@sveltecasts/svelte-youtube"

	var videos = []
	var sortedVideos = []
	var channelIds = ["UCFwMITSkc1Fms6PoJoh1OUQ", "UCSUu1lih2RifWkKtDOJdsBA"]

	function getVideos(channelId) {
		return new Promise((resolve, reject) => {
			gapi.load('auth2', function() {
				fetch(`https://www.googleapis.com/youtube/v3/search?key=AIzaSyAuXmYoR-lC_1mauhYNkOg_zcVO3-uikvk&channelId=${channelId}&part=snippet,id&order=date&maxResults=20`)
					.then(response => {
						return response.json()
					})
					.then(data => {
						console.log(data)
						let videos = []
						for(let video of data.items) {
							videos.push(video)
						}
						resolve(videos)
					})
			})
		})
	}

	async function init() {
		for(let id of channelIds) {
			let channelVideos = await getVideos(id)
			for(let vid of channelVideos) {
				vid.snippet.publishTime = new Date(vid.snippet.publishTime.split("T")[0])
				videos.push(vid)
			}
		}
		sortedVideos = videos.sort((a, b) => {
			if(a.snippet.publishTime > b.snippet.publishTime) return -1
			if(b.snippet.publishTime > a.snippet.publishTime) return 1
			return 0
		})
		console.log(sortedVideos)
	}

	init()
</script>

<main>
	<Titlebar text="Space Eggs"></Titlebar>
	<div class="content">
		{#if sortedVideos.length > 0}
			{#each sortedVideos as video}
				<Item title={video.snippet.channelTitle} date={video.snippet.publishTime.getMonth() + "/" + video.snippet.publishTime.getDate() + "/" + video.snippet.publishTime.getYear()} videoId={video.id.videoId} type="Youtube"></Item>
			{/each}
		{/if}
	</div>
</main>

<style>
	main {
		text-align: center;
		max-width: 240px;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	.content {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>