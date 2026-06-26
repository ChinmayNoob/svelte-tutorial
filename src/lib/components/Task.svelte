<script lang="ts">
	let { text, completed = false, onDelete } = $props();
</script>

<div style="display: flex; align-items: center; padding: 8px; margin: 5px 0; background: #f5f5f5; border-radius: 4px;">
	<input type="checkbox" bind:checked={completed} style="margin-right: 10px;" />
	<span style="flex: 1; text-decoration: completed ? 'line-through' : 'none'; color: completed ? '#999' : '#333';">
		{text}
	</span>
	<button onclick={onDelete} style="margin-left: 10px; padding: 4px 8px; background: #ff6b6b; color: white; border: none; border-radius: 4px; cursor: pointer;">✕</button>
</div>