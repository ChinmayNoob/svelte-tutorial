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
	<div class="card-header">
		<h3 class="card-title">{title}</h3>
		<span class="card-count-badge">{cardCount}</span>
	</div>
	<p class="card-description">{description}</p>
	<div class="card-footer">
		<span class="card-count-text">{cardCount} cards</span>
		<span class="card-status">{cardCount > 5 ? 'Busy' : 'Active'}</span>
	</div>
</div>

<style>
	.card {
		border: 2px solid #e0e0e0;
		padding: 16px;
		margin: 8px 0;
		border-radius: 8px;
		background: white;
		transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
		position: relative;
		overflow: hidden;
	}

	.card::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 3px;
		background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
		opacity: 0;
		transition: opacity 0.3s ease;
	}

	.card:hover::before {
		opacity: 1;
	}

	.card:hover {
		transform: translateY(-4px);
		box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
		border-color: #667eea;
	}

	.card.highlighted {
		background: linear-gradient(135deg, #fff9c4 0%, #fff59d 100%);
		border-color: #ffd700;
	}

	.card.highlighted::before {
		background: linear-gradient(90deg, #ffd700 0%, #ffb300 100%);
		opacity: 1;
	}

	.card-header {
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		margin-bottom: 12px;
	}

	.card-title {
		margin: 0;
		font-size: 16px;
		font-weight: 600;
		color: #333;
		line-height: 1.3;
	}

	.card-count-badge {
		background: #667eea;
		color: white;
		padding: 4px 8px;
		border-radius: 12px;
		font-size: 12px;
		font-weight: 600;
	}

	.card.highlighted .card-count-badge {
		background: #ffd700;
		color: #333;
	}

	.card-description {
		color: #666;
		margin: 0 0 12px 0;
		font-size: 14px;
		line-height: 1.5;
		min-height: 42px;
	}

	.card-footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-top: 12px;
		border-top: 1px solid #f0f0f0;
	}

	.card-count-text {
		color: #999;
		font-size: 13px;
		font-weight: 500;
	}

	.card-status {
		font-size: 12px;
		padding: 2px 8px;
		border-radius: 4px;
		background: #e3f2fd;
		color: #1976d2;
		font-weight: 500;
	}

	.card.highlighted .card-status {
		background: #fff3e0;
		color: #f57c00;
	}
</style>