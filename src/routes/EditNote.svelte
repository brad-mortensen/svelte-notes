<script>
  import { onMount } from "svelte";
  import { Link } from "svelte-routing";
  const noteId = `${window.location.pathname.slice(
    6,
    window.location.pathname.length
  )}`;
  console.log(`state: ${window.history.state.toString()}`);
  let currentNote = [];
  const fetchNote = async id => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${noteId}`
    );
    const data = await response.json();
    return data;
  };
  onMount(async () => {
    await fetchNote()
      .then(data => (currentNote = data))
      .catch(err => console.log(`Error getting single note: ${err}`));
  });
</script>

<style>

</style>

<form class="form">
  <h3>Edit Note:</h3>
  <input placeholder="Note Title" bind:value={currentNote.title} />
  <textarea class="body" placeholder="Note Content" bind:value={currentNote.textBody} />
  <button class="save">Save</button>
</form>
