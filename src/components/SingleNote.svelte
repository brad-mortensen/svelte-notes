<script>
  let currentNote = [];
  const fetchNote = async id => {
    const response = await fetch(
      `https://lambda-notes-build.herokuapp.com/api/notes/${id}`
    );
    const data = await response.json();
  };
</script>

<style>

</style>

<div class="single-note">
  <h1 class="title">Note Title</h1>
  <p class="textBody">Note BOdy</p>
</div>
