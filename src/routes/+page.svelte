<script lang="ts">
	import Card from '$lib/components/Card.svelte';
</script>

<div style="padding: 20px;">
	<h1>Phase 2: Component Architecture - Step 2</h1>
	<p style="margin: 10px 0;"><a href="/phase1">← View Phase 1 implementation</a></p>

	<h2>Multiple Props Card Component</h2>
	<p>Learning TypeScript interfaces, optional props, and default values</p>

	<hr style="margin: 20px 0;" />

	<h3>Card Examples with Different Props:</h3>

	<h4>Basic card with just title:</h4>
	<Card title="Simple Card" />

	<h4>Card with title and description:</h4>
	<Card title="Task Card" description="This card has a custom description" />

	<h4>Card with all props:</h4>
	<Card title="Full Card" description="Complete card with all features" cardCount={5} />

	<h4>Card with many tasks:</h4>
	<Card title="Busy Card" description="This card has many tasks" cardCount={12} />

	<hr style="margin: 20px 0;" />

</div>