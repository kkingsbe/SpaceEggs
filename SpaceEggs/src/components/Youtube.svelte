<script>
  export let videoId
</script>

<main>
  <iframe frameborder="0" allowfullscreen="1" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" title="YouTube video player" width="640" height="390" src="https://www.youtube.com/embed/{videoId}?enablejsapi=1&amp;widgetid=1"></iframe>
</main>

<style>
  main {
    width: fit-content;
  }
</style>