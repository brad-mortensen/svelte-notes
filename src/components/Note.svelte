<script>
  export let note;
  const handleDelete = async e => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${e.target.id}`,
      { method: "DELETE" }
    );
    console.log(response.status);
  };
</script>

<style>
  .note {
    background: white;
    width: 250px;
    height: 250px;
    padding: 10px;
    margin-bottom: 20px;
    border: 3px solid lightsalmon;
    overflow: scroll;
  }
  .note h2 {
    font-size: 2rem;
  }
  .note p {
    font-size: 1.2rem;
  }
</style>

<div class="note">
  <span class="delete" id={note.id} on:click={handleDelete}>X</span>
  <h2>{note.title}</h2>
  <p>{note.textBody}</p>
</div>
