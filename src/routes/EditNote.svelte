<script>
  import { onMount } from "svelte";
  import { Link,  navigate} from "svelte-routing";
  import { api } from "../extras/extras";

  export let id;

  let currentNote = [];

  const handleEdit = async e => {
    e.preventDefault();
    const { id } = currentNote;
    const data = { 
      title: currentNote.title, 
      textBody: currentNote.textBody 
    };
    const options = {
      method: "PUT",
      body: JSON.stringify(data),
      headers: {
        "Content-Type": "application/json"
      }
    };
    await fetch(`${api}${id}`, options)
      .then(res => {
        console.log(res.status);
        navigate(`/note/${id}`, { replace: true });
      })
      .catch(err => console.error(err));
  };

  const fetchNote = async () => {
    const response = await fetch(`${api}${id}`);
    return response.json();
  };
  onMount(async () => {
    await fetchNote()
      .then(data => currentNote = data)
      .catch(err => console.error(`Error getting single note: ${err}`));
  });
</script>

<style>
  .edit-container {
    background: linen;
    width: 60%;
    display: flex;
    flex-flow: column;
    margin-top: 90px;
  }
  .edit-container .back {
    width: 100%;
    text-align: right;
    padding-right: 20px;
    font-size: 12px;
  }
  .edit-container h2 {
    width: 100%;
    text-align: center;
    font-size: 1.8rem;
  }
  .edit-container .edit-form {
    display: flex;
    flex-flow: column;
    align-items: center;
    font-size: 1rem;
  }
  .edit-container .edit-form .title {
    width: 60%;
    margin-bottom: 20px;
    height: 40px;
  }
  .edit-container .edit-form .textBody {
    width: 60%;
    margin-bottom: 20px;
    height: 200px;
    resize: none;
  }
  .edit-container .edit-form button {
    width: 28%;
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

<div class="edit-container">
  <Link to={`/note/${currentNote.id}`}>
    <p class="back">Back</p>
  </Link>
  <h2>Edit Note:</h2>
  <form class="edit-form">
    <input
      class="title"
      placeholder="Note Title"
      bind:value={currentNote.title} />
    <textarea
      class="textBody"
      placeholder="Note Content"
      bind:value={currentNote.textBody} />
    <button class="save btn" on:click={handleEdit}>Save</button>
  </form>
</div>
