<script>
  import { onMount } from "svelte";
  import { Link } from "svelte-routing";
  import { api } from "../extras/extras";
  import Note from "./Note.svelte";
  import SingleNote from "./SingleNote.svelte";

  let pageRange = [];
  let currentPage = 1;
  let notesPerPage = 6;
  let newNotes;
  let notes = [];

  const fetchNotes = async () => {
    const response = await fetch(api);
    const data = await response.json();
    return data;
  };

  const setPageNum = e => {
    currentPage = e.target.innerText;
  };

  $: sortedNotesAZ = [...notes].sort((a, b) =>
    a.title > b.title ? 1 : b.title > a.title ? -1 : 0
  );

  $: sortedNotesZA = [...notes].sort((b, a) =>
    a.title > b.title ? 1 : b.title > a.title ? -1 : 0
  );

  const handleSort = e => {
    const inner = e.target.innerText;
    inner === "Sort A-Z" ? (notes = sortedNotesAZ) : (notes = sortedNotesZA);
    sorted = !sorted;
  };

  let sorted = false;

  onMount(async () => {
    await fetchNotes()
      .then(data => {
        notes = [...data];
        notesPerPage = notes.length;
      })
      .catch(err => console.error(`Error getting Notes: ${err}`));
    for (let i = 1; i <= Math.ceil(notes.length / notesPerPage); i++) {
      pageRange.push(i);
    }
    newNotes = notes.slice(
      currentPage * notesPerPage - notesPerPage,
      currentPage * notesPerPage
    );
    notes = newNotes;
  });
</script>

<style>
  .notes-container {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    padding: 0 20px;
    max-width: 1200px;
  }
  .notes-container .page-numbers {
    font-size: 1rem;
    width: 100%;
    text-align: right;
    margin: 20px;
    margin-top: 0;
    box-sizing: border-box;
  }
  .notes-container .page-numbers span {
    margin-left: 25px;
    cursor: pointer;
  }
  .notes-container .page-numbers .current-page {
    font-size: 1.2rem;
    font-weight: bold;
  }
</style>

<div class="notes-container">
  <div class="page-numbers">
    <button on:click|preventDefault={handleSort}>
      {sorted ? 'Sort Z-A' : 'Sort A-Z'}
    </button>
    {#each pageRange as num (currentPage)}
      {#if num === currentPage}
        <span class="current-page">{num}</span>
      {:else}
        <span on:click={setPageNum}>{num}</span>
      {/if}
    {/each}
  </div>

  {#each notes as note (notes)}
    <Note {note} />
  {:else}
    <p>*No notes yet*</p>
    <Link to="/add-note">
      <p>Add a Note</p>
    </Link>
  {/each}
</div>
