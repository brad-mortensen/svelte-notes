<script>
  import { onMount } from "svelte";
  import {api} from "../extras/extras";
  import Note from "./Note.svelte";
  import SingleNote from "./SingleNote.svelte";
  $: pageRange = [];
  $: currentPage = 1;
  let notesPerPage = 6;
  let newNotes;
  $: notes = [];
  const fetchNotes = async () => {
    const response = await fetch(api);
    const data = await response.json();
    return data;
  };
  const setPageNum = e => {
    currentPage = e.target.innerText;
  };
  onMount(async () => {
    await fetchNotes()
      .then(data => (notes = [...data]))
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
    <p>Sort</p>
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
  {/each}
</div>
