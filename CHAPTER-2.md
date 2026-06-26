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

---

# Chapter 8: Multiple Props with TypeScript Interfaces

## What you learned:
- TypeScript interfaces for type-safe props
- Optional props with `?` syntax
- Default values using `=` in destructuring
- Multiple props with different data types

## React comparison:
```jsx
// React
interface CardProps {
  title: string;
  description?: string;
  cardCount?: number;
}

export default function Card({ title, description = 'No description', cardCount = 0 }: CardProps) {
  return (
    <div>
      <h3>{title}</h3>
      <p>{description}</p>
      <p>Cards: {cardCount}</p>
    </div>
  );
}

// Svelte 5
<script lang="ts">
  interface CardProps {
    title: string;
    description?: string;
    cardCount?: number;
  }

  let { title, description = 'No description provided', cardCount = 0 }: CardProps = $props();
</script>

<div>
  <h3>{title}</h3>
  <p>{description}</p>
  <p>Cards: {cardCount}</p>
</div>
```

## Key differences:
- Same TypeScript syntax for interfaces
- Default values set directly in destructuring
- Props accessed directly without `props.` prefix
- Cleaner, more readable component code