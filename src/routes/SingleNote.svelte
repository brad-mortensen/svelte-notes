<script>
  import { onMount } from "svelte";
  const noteId = `${window.location.pathname.slice(
    6,
    window.location.pathname.length
  )}`;
  console.log(`noteId: ${noteId}`);
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
  .single-note {
    background-color: white;
  }
</style>

<div class="single-note">
  <h1 class="title">{currentNote.title}</h1>
  <p class="textBody">{currentNote.textBody}</p>
</div>
