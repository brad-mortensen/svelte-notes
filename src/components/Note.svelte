<script>
  export let note;
  const handleDelete = () => {
    
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
  <span class="delete" on:click={handleDelete}>X</span>
</div>
