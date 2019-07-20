<script>
  export let adding;
</script>

<style>
  .add-note-container {
    background: white;
    width: 60%; 
    display: flex;
    flex-flow: column;  
  }
</style>

<div class="add-note-container">
  <h2>Add a note</h2>
  <form>
    <input class="title" type="text"/>
    <textarea class="body" type="text"/>
  </form>
</div>
