<script>
	import Nav from './components/Nav.svelte';
	import NotesList from './components/NotesList.svelte';
	export let name;
</script>

<style>
.app {
	max-width: 100%;
	box-sizing: border-box;
}
.app .container {
	max-width: 1200px;
	margin: 0 auto;
}
</style>
<div class="app">
	<Nav />
	<div class="container">
		<NotesList/>
	</div>
</div>

