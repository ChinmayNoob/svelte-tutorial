<script lang="ts">
	interface CardProps {
		title: string;
		description?: string;
		cardCount?: number;
	}

	let { title, description = 'No description provided', cardCount = 0 }: CardProps = $props();
</script>

<div style="border: 2px solid #333; padding: 15px; margin: 10px 0; border-radius: 8px;">
	<h3 style="margin: 0 0 10px 0;">{title}</h3>
	<p style="color: #666; margin: 0 0 10px 0;">{description}</p>
	<p style="color: #999; font-size: 14px; margin: 0;">Cards: {cardCount}</p>
</div>