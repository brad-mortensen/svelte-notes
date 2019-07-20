<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  const toggleTrue = () => {
    dispatch("toggleTrue");
  };

  const toggleFalse = () => {
    dispatch("toggleFalse");
  };
</script>

<style>
  .nav-bar {
    width: 100%;
    margin: 0;
    padding: 0 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: white;
  }
  .nav-bar h1 {
    color: forestgreen;
    width: 50%;
    font-size: 2rem;
  }
  .nav-bar .nav-buttons {
    display: flex;
    justify-content: flex-end;
    width: 50%;
  }
  .nav-bar .nav-buttons p {
    margin-left: 25px;
    font-size: 1rem;
    cursor: pointer;
  }
</style>

<div class="nav-bar">
  <h1>Svelte Notes</h1>
  <div class="nav-buttons">
    <p on:click={toggleFalse}>View Notes</p>
    <p on:click={toggleTrue}>New Note</p>
  </div>
</div>
