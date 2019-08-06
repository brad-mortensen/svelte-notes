<script>
  import { onMount } from "svelte";
  import { Link } from "svelte-routing";
  const noteId = `${window.location.pathname.slice(
    6,
    window.location.pathname.length
  )}`;
  console.log(`noteId: ${noteId}`);
  let currentNote = [];
  const fetchNote = async id => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${noteId}`
    );
    const data = await response.json();
    return data;
  };
  let deleting = false;
  const handleDelete = async () => {
    await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${noteId}`,
      { method: "DELETE" }
    )
      .then(res => console.log(res.status))
      .catch(err => console.log(err));
  };
  onMount(async () => {
    await fetchNote()
      .then(data => (currentNote = data))
      .catch(err => console.log(`Error getting single note: ${err}`));
  });
</script>
<style></style>
<h1>Edit Notes</h1>