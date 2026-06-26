<script lang="ts">
	import Card from '$lib/components/Card.svelte';
	import Task from '$lib/components/Task.svelte';

	let tasks = $state([
		{ id: 1, text: 'Learn Svelte basics', completed: true },
		{ id: 2, text: 'Build components', completed: false },
		{ id: 3, text: 'Master state management', completed: false }
	]);

	function deleteTask(id: number) {
		tasks = tasks.filter(task => task.id !== id);
	}
</script>

<div class="container">
	<h1>Phase 3: Styling & Tailwind - Step 2 & 3</h1>
	<p><a href="/phase1">← View Phase 1 implementation</a></p>

	<h2>Tailwind CSS & Dynamic Classes</h2>
	<p>Learning Tailwind utilities and conditional styling with class: directive</p>

	<hr />

	<h3>Card Examples:</h3>

	<h4>Basic cards:</h4>
	<Card title="Regular Card" description="Standard card styling" cardCount={2} />

	<h4>Highlighted cards (dynamic classes):</h4>
	<Card title="Important Card" description="This card is highlighted" cardCount={5} highlighted={true} />
	<Card title="Urgent Task" description="Needs attention" cardCount={8} highlighted={true} />

	<h4>Normal card for comparison:</h4>
	<Card title="Normal Card" description="No highlighting" cardCount={1} highlighted={false} />

	<hr />

	<h3>Task Component (inline styles for comparison):</h3>

	<h4>Simple tasks:</h4>
	<Task text="Buy groceries" completed={true} />
	<Task text="Walk the dog" completed={false} />
	<Task text="Read documentation" />

	<hr />

	<h4>Tasks with delete events:</h4>
	{#each tasks as task (task.id)}
		<Task text={task.text} completed={task.completed} onDelete={() => deleteTask(task.id)} />
	{/each}

	{#if tasks.length === 0}
		<p class="empty-state">No tasks left!</p>
	{/if}

	<hr />

</div>

<style>
	.container {
		padding: 20px;
	}

	hr {
		margin: 20px 0;
	}

	h4 {
		margin: 10px 0;
	}

	.empty-state {
		color: #666;
		margin: 10px 0;
	}

	h3 {
		margin: 15px 0 5px 0;
	}
</style>