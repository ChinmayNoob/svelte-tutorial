# Chapter 7: Creating Basic Components

## What you learned:
- Component file structure: `.svelte` files with `<script>` and template
- `$props()` rune to accept props in Svelte 5
- Import components: `import Card from '$lib/components/Card.svelte'`
- Use components: `<Card title="My Title" />`

## React comparison:
```jsx
// React - Card.jsx
export default function Card({ title }) {
  return (
    <div>
      <h3>{title}</h3>
    </div>
  );
}

// Usage
import Card from './Card';
<Card title="My Title" />

// Svelte 5 - Card.svelte
<script lang="ts">
  let { title } = $props();
</script>

<div>
  <h3>{title}</h3>
</div>

// Usage
import Card from '$lib/components/Card.svelte';
<Card title="My Title" />
```

## Key differences:
- No export statement needed for components
- Props destructured directly in `$props()`
- Script section separate from template
- More intuitive file structure