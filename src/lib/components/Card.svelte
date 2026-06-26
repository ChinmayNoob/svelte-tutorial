<script lang="ts">
	interface CardProps {
		title: string;
		description?: string;
		cardCount?: number;
		highlighted?: boolean;
	}

	let { title, description = 'No description provided', cardCount = 0, highlighted = false }: CardProps = $props();
</script>

<div class="card" class:highlighted={highlighted}>
	<h3>{title}</h3>
	<p class="description">{description}</p>
	<p class="count">Cards: {cardCount}</p>
</div>

<style>
	.card {
		border: 2px solid #333;
		padding: 15px;
		margin: 10px 0;
		border-radius: 8px;
		background: white;
	}

	.card.highlighted {
		background: #fffacd;
		border-color: #ffd700;
	}

	.description {
		color: #666;
		margin: 10px 0;
	}

	.count {
		color: #999;
		font-size: 14px;
		margin: 0;
	}
</style>