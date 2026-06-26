<script lang="ts">
	let { text, completed = false, onDelete } = $props();
</script>

<div class="task">
	<input type="checkbox" bind:checked={completed} class="checkbox" />
	<span class="task-text" class:completed={completed}>
		{text}
	</span>
	<button onclick={onDelete} class="delete-btn">✕</button>
</div>

<style>
	.task {
		display: flex;
		align-items: center;
		padding: 12px;
		margin: 8px 0;
		background: #f8f9fa;
		border-radius: 6px;
		border: 1px solid #e9ecef;
		transition: all 0.2s ease;
	}

	.task:hover {
		background: #fff;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
		border-color: #dee2e6;
		transform: translateX(2px);
	}

	.checkbox {
		margin-right: 12px;
		width: 18px;
		height: 18px;
		cursor: pointer;
		accent-color: #4CAF50;
	}

	.task-text {
		flex: 1;
		color: #333;
		font-size: 14px;
		transition: all 0.2s ease;
	}

	.task-text.completed {
		text-decoration: line-through;
		color: #999;
		font-style: italic;
	}

	.delete-btn {
		margin-left: 12px;
		padding: 6px 10px;
		background: #ff6b6b;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-size: 14px;
		transition: all 0.2s ease;
		opacity: 0;
		transform: scale(0.9);
	}

	.task:hover .delete-btn {
		opacity: 1;
		transform: scale(1);
	}

	.delete-btn:hover {
		background: #ff5252;
		transform: scale(1.05);
	}

	.delete-btn:active {
		transform: scale(0.95);
	}
</style>