<script>
  import { Link } from "svelte-routing";

  export let note;
  const handleDelete = async e => {
    await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${e.target.id}`,
      { method: "DELETE" }
    )
      .then(res => console.log(res.status))
      .catch(err => console.log(`error deleting note: ${err}`));
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
  <h2>{note.title}</h2>
  <p>{note.textBody}</p>
</div>
