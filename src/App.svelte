<script lang="ts">
	import TodoList from './TodoList.svelte';
	import { Styles } from 'sveltestrap';
</script>

<main>
	<Styles />
	<TodoList />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		display: flex;
		justify-content: center;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
