<script>
  import { onMount } from "svelte";
  import Note from "./Note.svelte";
  let pageRange = [];
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
    for (let i = 1; i <= Math.ceil(notes.length / notesPerPage); i++) {
      pageRange.push(i);
    }
    console.log(`pageRange: ${pageRange}`);
    let newNotes = notes.slice(
      currentPage * notesPerPage - notesPerPage,
      currentPage * notesPerPage
    );
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
  .notes-container .page-numbers {
    font-size: 1rem;
    width: 100%;
    text-align: right;
  }
  .notes-container .page-numbers span {
    margin-left: 10px;
    cursor: pointer;
  }
</style>

<div class="notes-container">
  <div class="page-numbers">
    {#each pageRange as num (num)}
      <span>{num}</span>
    {/each}
  </div>

  {#each notes as note}
    <Note {note} />
  {:else}
    <p>*No notes yet*</p>
  {/each}
</div>
