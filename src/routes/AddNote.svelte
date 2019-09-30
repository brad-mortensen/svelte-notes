<script>
  import { onMount } from "svelte";

  let title = "";
  let textBody = "";
  const handleSubmit = e => {
    e.preventDefault();
    const data = { title, textBody };
    const options = {
      method: "POST",
      body: JSON.stringify(data),
      headers: {
        "Content-Type": "application/json"
      }
    };
    fetch("https://lambda-notes-build.herokuapp.com/api/notes", options)
      .then(res => console.log(res.status))
      .catch(err => console.error(err));
    window.history.back();
  };
</script>

<style>
  .add-note-container {
    background: white;
    width: 60%;
    display: flex;
    flex-flow: column;
    margin-top: 85px;
  }
  .add-note-container h2 {
    width: 100%;
    text-align: center;
    font-size: 2rem;
  }
  .add-note-container .new-note-form {
    display: flex;
    flex-flow: column;
    align-items: center;
    font-size: 1rem;
  }
  .add-note-container .new-note-form .title {
    width: 60%;
    margin-bottom: 20px;
    height: 40px;
  }
  .add-note-container .new-note-form .textBody {
    width: 60%;
    margin-bottom: 20px;
    height: 200px;
    resize: none;
  }
  .add-note-container .new-note-form .save {
    width: 25%;
    height: 40px;
    background-color: white;
    font-size: 1.4rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: forestgreen;
    color: white;
  }
</style>

<div class="add-note-container">
  <h2>Add a note</h2>
  <form class="new-note-form">
    <input
      class="title"
      type="text"
      bind:value={title}
      placeholder="Enter title..." />
    <textarea
      class="textBody"
      type="text"
      bind:value={textBody}
      placeholder="Enter Note Content..." />
    <p class="save"type="submit" on:click={handleSubmit}>SAVE</p>
  </form>
</div>
