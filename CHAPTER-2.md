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

---

# Chapter 9: Task Component with Two-Way Binding

## What you learned:
- Boolean props for checkbox state
- Two-way binding with `bind:checked`
- Reactive state synchronization between parent and child
- Conditional styling based on prop values

## React comparison:
```jsx
// React
export default function Task({ text, completed, onCompleted }) {
  return (
    <div>
      <input
        type="checkbox"
        checked={completed}
        onChange={(e) => onCompleted(e.target.checked)}
      />
      <span style={{ textDecoration: completed ? 'line-through' : 'none' }}>
        {text}
      </span>
    </div>
  );
}

// Svelte 5
<script lang="ts">
  let { text, completed = false } = $props();
</script>

<div>
  <input type="checkbox" bind:checked={completed} />
  <span style="text-decoration: completed ? 'line-through' : 'none';">
    {text}
  </span>
</div>
```

## Key differences:
- `bind:checked` replaces `checked` + `onChange`
- No need for callback functions
- Automatic two-way synchronization
- Much cleaner syntax for form elements

---

# Chapter 10: Component Events & Parent-Child Communication

## What you learned:
- Event handling via callback props in Svelte 5
- Parent functions passed as props to children
- Child components trigger parent actions
- No need for `createEventDispatcher()` in modern Svelte 5

## React comparison:
```jsx
// React
export default function Task({ text, completed, onDelete }) {
  return (
    <div>
      <input type="checkbox" checked={completed} />
      <span>{text}</span>
      <button onClick={onDelete}>✕</button>
    </div>
  );
}

// Parent component
function App() {
  const handleDelete = (id) => {
    setTasks(tasks.filter(t => t.id !== id));
  };

  return <Task onDelete={() => handleDelete(task.id)} />;
}

// Svelte 5
<script lang="ts">
  let { text, completed = false, onDelete } = $props();
</script>

<div>
  <input type="checkbox" bind:checked={completed} />
  <span>{text}</span>
  <button onclick={onDelete}>✕</button>
</div>

// Parent component
<script lang="ts">
  function deleteTask(id: number) {
    tasks = tasks.filter(task => task.id !== id);
  }
</script>

<Task onDelete={() => deleteTask(task.id)} />
```

## Key differences:
- Callback functions work the same way as React
- No need for `createEventDispatcher()` in Svelte 5
- Cleaner prop naming (`onDelete` vs dispatching custom events)
- More intuitive parent-child communication