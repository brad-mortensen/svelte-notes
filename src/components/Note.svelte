<script>
  export let note;
  const handleDelete = async e => {
    console.log(e.target.id);
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${e.target.id}`,
      { method: "DELETE" }
    );
    return response.status;
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
  }
  .note h2 {
    font-size: 2rem;
  }
  .note p {
    font-size: 1.2rem;
  }
</style>

<div class="note">
  <h2>{note.title}</h2>
  <p>{note.textBody}</p>
  <span class="delete" id={note.id} on:click={handleDelete}>X</span>
</div>
