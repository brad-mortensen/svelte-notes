<script>
  import Nav from "./components/Nav.svelte";
  import NotesList from "./components/NotesList.svelte";
  export let name;
</script>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }

  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
      "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans",
      "Helvetica Neue", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 62.5%;
    box-sizing: border-box;
		background-color: lightsalmon;
  }

  :global(code) {
    font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
      monospace;
  }
  .app {
    max-width: 100%;
    box-sizing: border-box;
    
  }
  .app .container {
    max-width: 1200px;
    margin: 0 auto;
  }
</style>

<div class="app">
  <Nav />
  <div class="container">
    <NotesList />
  </div>
</div>
