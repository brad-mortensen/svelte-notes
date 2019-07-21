<script>
  import { onMount } from "svelte";
  import Note from "./Note.svelte";
  let currentPage = 1;
  let notesPerPage = 6;
  let notes = [];
  const fetchNotes = async () => {
    const response = await fetch(
      "https://lambda-notes-build.herokuapp.com/api/notes"
    );
    const data = await response.json();
    return data;
  };

  onMount(async () => {
    await fetchNotes().then(data => (notes = [...data]));
    let newNotes = notes.slice((currentPage * notesPerPage)-notesPerPage, currentPage * notesPerPage );
    notes = newNotes;
  });
</script>

<style>
  .notes-container {
    padding-top: 50px;
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    padding: 50px 20px;
  }
  .notes-container p {
    font-size: 3rem;
  }
</style>

<div class="notes-container">
  {#each notes as note, i}
    <Note {note} />
  {:else}
    <p>*No notes yet*</p>
  {/each}
</div>
