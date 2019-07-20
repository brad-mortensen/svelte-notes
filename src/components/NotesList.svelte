<script>
  import Note from "./Note.svelte";
  const notes = [
    {
      title: "tacos",
      body: "i likes to eat tacos",
      id: 0
    },
    {
      title: "burgers",
      body: "i ralso like burgrses",
      id: 1
    },
    {
      title: "candy",
      body: "i readlly like candies",
      id: 2
    }
  ];
</script>

<style>
  .notes-container {
    padding-top: 50px;
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    padding:50px 20px;
  }
</style>

<div class="notes-container">
  {#each notes as note, i}
    <Note {note} />
  {:else}
    <p>No notes yet.</p>
  {/each}
</div>
