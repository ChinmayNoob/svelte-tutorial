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

<div style="padding: 20px;">
	<h1>Phase 2: Component Architecture - Step 3 & 4</h1>
	<p style="margin: 10px 0;"><a href="/phase1">← View Phase 1 implementation</a></p>

	<h2>Task Component & Event Handling</h2>
	<p>Learning two-way binding, boolean props, and component events</p>

	<hr style="margin: 20px 0;" />

	<h3>Task Component Examples:</h3>

	<h4>Simple tasks (checkbox binding):</h4>
	<Task text="Buy groceries" completed={true} />
	<Task text="Walk the dog" completed={false} />
	<Task text="Read documentation" />

	<hr style="margin: 20px 0;" />

	<h4>Tasks with delete events:</h4>
	{#each tasks as task (task.id)}
		<Task text={task.text} completed={task.completed} onDelete={() => deleteTask(task.id)} />
	{/each}

	{#if tasks.length === 0}
		<p style="color: #666; margin: 10px 0;">No tasks left!</p>
	{/if}

	<hr style="margin: 20px 0;" />

</div>