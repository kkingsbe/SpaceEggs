<script>
  export let text
</script>

<main>
  <div class="titlebar">
    <p>{text}</p>
  </div>
</main>

<style>
  main {
    margin-bottom: 3em;
  }
  .titlebar {
    width: 100%;
    height: 5.6em;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid rgb(212, 212, 212);
    cursor: default;
  }
  p {
    margin: 0;
    color: rgb(41, 41, 41);
		font-size: 4em;
  }
</style>