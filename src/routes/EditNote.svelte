<script>
  import { onMount } from "svelte";
  import { Link } from "svelte-routing";
  const noteId = `${window.location.pathname.slice(
    6,
    window.location.pathname.length
  )}`;
  let currentNote = [];
  console.log(currentNote, "current");

  const handleEdit = async e => {
    e.preventDefault();
    const data = { title: currentNote.title, textBody: currentNote.textBody };
    const options = {
      method: "PUT",
      body: JSON.stringify(data),
      headers: {
        "Content-Type": "application/json"
      }
    };
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${e.target.id}`,
      options
    );
    console.log(response.status);
  };
  const fetchNote = async id => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${noteId}`
    );
    return await response.json();
  };
  onMount(async () => {
    await fetchNote()
      .then(data => (currentNote = data))
      .catch(err => console.log(`Error getting single note: ${err}`));
  });
</script>

<style>
  .edit-container {
    background: white;
    width: 60%;
    display: flex;
    flex-flow: column;
    margin-top: 85px;
  }
  .edit-container h2 {
    width: 100%;
    text-align: center;
    font-size: 2rem;
  }
  .edit-container .edit-form {
    display: flex;
    flex-flow: column;
    align-items: center;
    font-size: 1rem;
  }
  .edit-container .edit-form .title {
    width: 60%;
    margin-bottom: 20px;
    height: 40px;
  }
  .edit-container .edit-form .textBody {
    width: 60%;
    margin-bottom: 20px;
    height: 200px;
    resize: none;
  }
  .edit-container .edit-form button {
    width: 28%;
    height: 44px;
    background-color: white;
    font-size: 1.4rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: forestgreen;
    color: white;
  }
</style>

<div class="edit-container">
  <h2>Edit Note:</h2>
  <form class="edit-form">
    <input
      class="title"
      placeholder="Note Title"
      bind:value={currentNote.title} />
    <textarea
      class="textBody"
      placeholder="Note Content"
      bind:value={currentNote.textBody} />
    <button class="save" on:Click={handleEdit}>Save</button>
  </form>
</div>
