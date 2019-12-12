<script>
  import { onMount } from "svelte";
  import { Link, navigate } from "svelte-routing";
  import { api } from "../extras/extras";
  const noteId = `${window.location.pathname.slice(
    6,
    window.location.pathname.length
  )}`;
  let currentNote = [];
  const fetchNote = async id => {
    const response = await fetch(`${api}${noteId}`);
    return await response.json();
  };
  let deleting = false;
  const handleDelete = async () => {
    await fetch(`${api}${noteId}`, { method: "DELETE" })
      .then(res => {
        console.log(res.status);
        navigate("/", { replace: true });
      })
      .catch(err => console.error(err));
  };
  onMount(async () => {
    await fetchNote()
      .then(data => (currentNote = data))
      .catch(err => console.error(`Error getting single note: ${err}`));
  });
</script>

<style>
  .single-note {
    margin-top: 150px;
    background-color: white;
    width: 40%;
    padding: 10px;
  }
  .single-note .back {
    font-size: 12px;
    width: 100%;
    text-align: right;
    margin: 0;
    padding: 0;
  }
  .single-note h1 {
    font-size: 2rem;
  }
  .single-note p {
    font-size: 1rem;
  }
  .single-note .buttons {
    display: flex;
    justify-content: space-around;
  }
  .single-note .buttons p {
    cursor: pointer;
    color: black;
    text-decoration: none;
  }
  .single-note .delete-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(4, 0, 0, 0.7);
  }
  .single-note .delete-container .delete-modal {
    width: 45%;
    height: 150px;
    border: none;
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    background-color: white;
  }
  .single-note .delete-container .delete-modal p {
    width: 100%;
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
  }
  .single-note .delete-container .delete-modal button {
    font-family: "Courier New", Courier, monospace;
    background-color: #01410e;
    width: 30%;
    height: 45px;
    margin-top: 0;
    color: white;
    font-size: 0.8rem;
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
    border: none;
  }
  .single-note .delete-container .delete-modal .delete {
    background-color: rgb(254, 78, 78);
  }
</style>

{#if currentNote !== []}
  <div class="single-note">
    <Link to="/">
      <p class="back">Back</p>
    </Link>
    <h1 class="title">{currentNote.title}</h1>
    <p class="textBody">{currentNote.textBody}</p>
    <div class="buttons">
      <Link to="edit/{currentNote.id}">
        <p>Edit</p>
      </Link>
      <p on:click={() => (deleting = true)}>Delete</p>
    </div>
    {#if deleting}
      <div class="delete-container">
        <div class="delete-modal">
          <p>Are you sure you'd like to delete?</p>
          <button class="delete" on:click={handleDelete}>Delete</button>
          <button on:click={() => (deleting = false)}>Cancel</button>
        </div>
      </div>
    {/if}
  </div>
{:else}
  <h1>Note not found</h1>
{/if}
