<script>
  let currentNote = [];
  const fetchNote = async id => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${id}`
    );
    const data = await response.json();
    return data;
  };
  // onMount(async () => {
  //   await fetchNotes()
  //     .then(data => (currentNote = [...data]))
  //     .catch(err => console.log(`Error getting single note: ${err}`));
  // });
</script>

<style>

</style>

<div class="single-note">
  <h1 class="title">Note Title</h1>
  <p class="textBody">Note BOdy</p>
</div>
