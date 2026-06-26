<script lang="ts">
	let count = $state(0);
	let doubled = $derived(count * 2);
	let data = $state<string | null>(null);
	let loading = $state(false);

	let columns = $state([
		{ id: 1, title: 'Todo', cardCount: 0 },
		{ id: 2, title: 'In Progress', cardCount: 0 },
		{ id: 3, title: 'Done', cardCount: 0 }
	]);

	function addColumn() {
		const newId = Math.max(...columns.map(c => c.id)) + 1;
		columns = [...columns, { id: newId, title: `Column ${newId}`, cardCount: 0 }];
	}

	function removeColumn(id: number) {
		columns = columns.filter(col => col.id !== id);
	}

	function incrementCards(columnId: number) {
		columns = columns.map(col =>
			col.id === columnId ? { ...col, cardCount: col.cardCount + 1 } : col
		);
	}

	$effect(() => {
		if (count > 0) {
			loading = true;
			fetch(`https://jsonplaceholder.typicode.com/todos/${count}`)
				.then(res => res.json())
				.then(json => {
					data = JSON.stringify(json);
					loading = false;
				})
				.catch(err => {
					data = `Error: ${err.message}`;
					loading = false;
				});
		} else {
			data = null;
		}
	});

	function increment() {
		count++;
	}

	function decrement() {
		if (count > 0) count--;
	}
</script>

<div style="padding: 20px;">
	<h1>Basic Counter - Step 4</h1>
	<p style="margin: 10px 0;">Current count: <strong>{count}</strong></p>
	<p style="margin: 10px 0;">Doubled: <strong>{doubled}</strong></p>

	{#if count === 0}
		<p style="margin: 10px 0;">Status: <strong>Zero</strong></p>
	{:else if count < 5}
		<p style="margin: 10px 0;">Status: <strong>Low</strong></p>
	{:else if count < 10}
		<p style="margin: 10px 0;">Status: <strong>Medium</strong></p>
	{:else}
		<p style="margin: 10px 0;">Status: <strong>High</strong></p>
	{/if}

	<button onclick={increment} style="margin: 5px; padding: 10px;">+ Increment</button>
	<button onclick={decrement} style="margin: 5px; padding: 10px;">- Decrement</button>

	<hr style="margin: 20px 0;" />

	<h2>API Fetch Test with $effect</h2>
	{#if loading}
		<p>Loading data...</p>
	{:else if data}
		<div style="background: #f0f0f0; padding: 10px; font-size: 12px;">
			<pre>{data}</pre>
		</div>
	{:else}
		<p>Increment counter to fetch data</p>
	{/if}

	<hr style="margin: 20px 0;" />

	<h2>Board Structure - Step 4 & 5</h2>
	<button onclick={addColumn} style="margin: 5px; padding: 10px;">+ Add Column</button>

	{#if columns.length === 0}
		<p style="color: #666; margin: 10px 0;">No columns yet. Add one to get started!</p>
	{:else}
		{#each columns as column (column.id)}
			<div style="border: 1px solid #ccc; padding: 10px; margin: 5px 0; display: flex; justify-content: space-between; align-items: center;">
				<div>
					<strong>{column.title}</strong> (ID: {column.id})
					<br />
					{#if column.cardCount === 0}
						<span style="color: #999;">No cards</span>
					{:else if column.cardCount < 5}
						<span style="color: #4CAF50;">{column.cardCount} cards - Getting started!</span>
					{:else}
						<span style="color: #2196F3;">{column.cardCount} cards - Great progress!</span>
					{/if}
				</div>
				<div>
					<button onclick={() => incrementCards(column.id)} style="margin: 2px; padding: 5px;">+ Cards</button>
					<button onclick={() => removeColumn(column.id)} style="margin: 2px; padding: 5px; background: #ff6b6b;">Remove</button>
				</div>
			</div>
		{/each}
	{/if}
</div>