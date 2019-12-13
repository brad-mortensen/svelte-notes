<script>
  import { Router, Route } from "svelte-routing";
  import Nav from "./components/Nav.svelte";
  import NotesList from "./routes/NotesList.svelte";
  import AddNote from "./routes/AddNote.svelte";
  import SingleNote from "./routes/SingleNote.svelte";
  import EditNote from "./routes/EditNote.svelte";
</script>

<style>
  :global(html) {
    scroll-behavior: smooth;
    box-sizing: border-box;
  }
  :global(*, *:before, *:after) {
    box-sizing: inherit;
  }
  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
      "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans",
      "Helvetica Neue", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 62.5%;
    background-color: lightsalmon;
    padding: 0;
    height: 100vh;
  }

  :global(code) {
    font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
      monospace;
  }
  .app {
    max-width: 100%;
  }
  .app .container {
    max-width: 1200px;
    height: 100%;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    box-sizing: border-box;
  }
</style>

<Router>
  <div class="app">
    <Nav />
    <div class="container">
      <Route path="/" component={NotesList}/>
      <Route path="add-note" component={AddNote} />
      <Route path="note/:id" let:params>
        <SingleNote id="{params.id}"/>
      </Route>
      <Route path="edit/:id" let:params>
        <EditNote id="{params.id}" />
      </Route>
    </div>
  </div>
</Router>
