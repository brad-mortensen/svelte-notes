<script>
  export let adding;
  let title = "";
  let textBody = "";
  console.log(`textBody: ${textBody}, title: ${title}`);
</script>

<style>
  .add-note-container {
    background: white;
    width: 60%;
    display: flex;
    flex-flow: column;
  }
  .add-note-container h2 {
    width: 100%;
    text-align: center;
    font-size: 2rem;
  }
  .add-note-container .new-note-form {
    display: flex;
    flex-flow: column;
  }
  .add-note-container .new-note-form .title {
    width: 60%;
  }
  .add-note-container .new-note-form .textBody {
    width: 60%;
  }
</style>

<div class="add-note-container">
  <h2>Add a note</h2>
  <form class="new-note-form">
    <input class="title" type="text" bind:value={title} />
    <textarea class="textBody" type="text" bind:value={textBody} />
    <button type="submit"></button>
  </form>
</div>
