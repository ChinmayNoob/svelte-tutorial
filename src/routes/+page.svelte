<script lang="ts">
	import Card from '$lib/components/Card.svelte';
	import Task from '$lib/components/Task.svelte';

	let columns = $state([
		{ id: 1, title: 'Todo', cards: 3, color: '#e0f2f1' },
		{ id: 2, title: 'In Progress', cards: 2, color: '#e8f5e9' },
		{ id: 3, title: 'Done', cards: 5, color: '#f3e5f5' }
	]);

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
	<h1>Phase 3: Styling & Tailwind - Complete</h1>
	<p><a href="/phase1">← View Phase 1 implementation</a></p>

	<h2>Styled Kanban Board with Animations</h2>
	<p>Learning polished UI, hover effects, and responsive layouts</p>

	<hr />

	<h3>Kanban Board:</h3>
	<div class="board">
		{#each columns as column (column.id)}
			<div class="column" style="background: {column.color}">
				<div class="column-header">
					<h3>{column.title}</h3>
					<span class="card-count">{column.cards} cards</span>
				</div>

				<div class="column-content">
					<Card title="Card 1" description="Sample task description" cardCount={2} />
					<Card title="Card 2" description="Another important task" cardCount={1} highlighted={true} />
					<Card title="Card 3" description="Regular task card" cardCount={3} />
					<Card title="Card 4" description="Additional task item" cardCount={4} highlighted={true} />
				</div>
			</div>
		{/each}
	</div>

	<hr />

	<h3>Task List with Hover Effects:</h3>
	<div class="task-list">
		{#each tasks as task (task.id)}
			<Task text={task.text} completed={task.completed} onDelete={() => deleteTask(task.id)} />
		{/each}

		{#if tasks.length === 0}
			<p class="empty-state">No tasks left!</p>
		{/if}
	</div>

	<hr />

</div>

<style>
	.container {
		padding: 24px;
		max-width: 1400px;
		margin: 0 auto;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
	}

	h1 {
		margin: 0 0 8px 0;
		font-size: 28px;
		color: #333;
	}

	h2 {
		margin: 0 0 4px 0;
		font-size: 20px;
		color: #666;
		font-weight: 500;
	}

	h3 {
		margin: 16px 0 8px 0;
		font-size: 18px;
		color: #333;
	}

	hr {
		margin: 24px 0;
		border: none;
		border-top: 2px solid #e0e0e0;
	}

	.board {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
		gap: 20px;
		margin: 20px 0;
	}

	.column {
		border-radius: 12px;
		padding: 16px;
		min-height: 420px;
		box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
		transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.column:hover {
		transform: translateY(-4px);
		box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
	}

	.column-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 16px;
		padding-bottom: 12px;
		border-bottom: 2px solid rgba(0, 0, 0, 0.1);
	}

	.column-header h3 {
		margin: 0;
		font-size: 18px;
		font-weight: 600;
		color: #333;
	}

	.card-count {
		background: rgba(0, 0, 0, 0.08);
		padding: 6px 12px;
		border-radius: 8px;
		font-size: 14px;
		font-weight: 600;
		color: #555;
	}

	.column-content {
		display: flex;
		flex-direction: column;
		gap: 12px;
	}

	.task-list {
		max-width: 640px;
		margin: 20px 0;
	}

	.empty-state {
		color: #999;
		margin: 24px 0;
		font-style: italic;
		text-align: center;
		padding: 20px;
		background: #f8f9fa;
		border-radius: 8px;
		border: 2px dashed #e0e0e0;
	}

	ul {
		line-height: 1.8;
		color: #555;
	}

	@media (max-width: 768px) {
		.container {
			padding: 16px;
		}

		.board {
			grid-template-columns: 1fr;
		}

		.column {
			min-height: auto;
		}

		h1 {
			font-size: 24px;
		}
	}
</style>