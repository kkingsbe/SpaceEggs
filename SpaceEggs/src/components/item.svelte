<script>
  export let title
  export let date
  export let type
  export let url
  export let videoId

  console.log(videoId)

  //import Youtube from "@sveltecasts/svelte-youtube"
  import Youtube from "./Youtube.svelte"
</script>

<main>
  <p class="title">{title}</p>
  <p class="date">{date}</p>
	<Youtube videoId={videoId}></Youtube>
</main>

<style>
  .title {
    width: 100;
    text-align: left;
    font-size: 1.8em;
    margin-bottom: 2px;
    padding-left: 5px;
  }
  .date {
    width: 100;
    text-align: left;
    font-size: 1em;
    margin-bottom: 5px;
    padding-left: 5px;
  }
</style>