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

</style>

<div>
  {#each notes as { note }, i}
    <Note {note} />
  {/each}
</div>
