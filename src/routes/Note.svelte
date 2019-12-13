<script>
  import { fly, fade } from 'svelte/transition';
  import { Link } from "svelte-routing";
  import {api} from "../extras/extras";
  export let note;
  const handleDelete = async e => {
    await fetch(`${api}${e.target.id}`, { method: "DELETE" })
      .then(res => console.log(res.status))
      .catch(err => console.error(`error deleting note: ${err}`));
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
    color: black;
    text-decoration: none;
  }
  .note:hover {
    text-decoration: none;
  }
  .note h2 {
    font-size: 2rem;
  }
  .note p {
    font-size: 1.2rem;
  }
</style>

<Link to="note/{note.id}">
  <div class="note" in:fly="{{ y: 200, duration: 500 }}">
    <h2>{note.title}</h2>
    <p>{note.textBody}</p>
  </div>
</Link>
