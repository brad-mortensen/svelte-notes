<script>
  import { onMount } from "svelte";
  import { navigate } from "svelte-routing";
  import { fly, fade } from "svelte/transition";
  import { api } from "../extras/extras";

  let title = "";
  let textBody = "";
  const handleSubmit = e => {
    const data = { title, textBody };
    const options = {
      method: "POST",
      body: JSON.stringify(data),
      headers: {
        "Content-Type": "application/json"
      }
    };
    fetch(api, options)
      .then(res => {
        console.log(res.status);
        navigate("/", { replace: true });
      })
      .catch(err => console.error(err));
  };
</script>

<style>
  .add-note-container {
    background: white;
    width: 60%;
    display: flex;
    flex-flow: column;
    margin-top: 80px;
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
    font-size: 1.2rem;
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

<div class="add-note-container" in:fly={{ y: 300, duration: 400 }}>
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
    <p class="save" type="submit" on:click={handleSubmit}>SAVE</p>
  </form>
</div>
