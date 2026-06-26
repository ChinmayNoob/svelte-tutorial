# Phase 3: Styling & Tailwind Integration

## Chapter 11: Svelte Scoped Styles

## What you learned:
- Add `<style>` section to Svelte components
- Scoped CSS only affects the component it's defined in
- No CSS pollution or naming conflicts
- Cleaner than inline styles for reusable components

## React comparison:
```jsx
// React - CSS Modules or styled-components
import styles from './Card.module.css';

export default function Card({ title }) {
  return (
    <div className={styles.card}>
      <h3>{title}</h3>
    </div>
  );
}

/* Card.module.css */
.card {
  border: 2px solid #333;
  padding: 15px;
}

// Svelte - Built-in scoped styles
<script lang="ts">
  let { title } = $props();
</script>

<div class="card">
  <h3>{title}</h3>
</div>

<style>
  .card {
    border: 2px solid #333;
    padding: 15px;
  }
</style>
```

## Key differences:
- No extra libraries or CSS modules needed
- Automatic scoping without configuration
- Write normal CSS, Svelte handles the scoping
- Much simpler than React's CSS-in-JS solutions

## How it works:
- Styles defined in `<style>` section only apply to that component
- No need for unique class names or CSS modules
- Cleaner component structure with built-in styling
- Better performance and developer experience

## When to use:
- Component-specific styles (most cases)
- When you want to avoid CSS conflicts
- For reusable components with consistent styling
- When you don't want global CSS pollution

---

## Chapter 12: Tailwind CSS Integration

## What you learned:
- Tailwind CSS already configured in the project
- Use Tailwind utility classes for rapid styling
- Replace custom CSS with Tailwind utilities
- Combine Tailwind with scoped styles when needed

## React comparison:
```jsx
// React
<div className="p-4 m-2 border-2 border-gray-800 rounded-lg">
  <h3 className="font-bold">{title}</h3>
</div>

// Svelte - Same syntax!
<div class="p-4 m-2 border-2 border-gray-800 rounded-lg">
  <h3 class="font-bold">{title}</h3>
</div>
```

## Key differences:
- Same Tailwind syntax as React
- Works seamlessly with Svelte components
- Can combine with scoped styles
- Faster development with existing Tailwind knowledge

## Common Tailwind classes:
- Spacing: `p-4` (padding), `m-2` (margin)
- Borders: `border-2`, `border-gray-800`
- Layout: `flex`, `grid`, `items-center`
- Colors: `text-white`, `bg-blue-500`
- Responsive: `md:p-8`, `lg:w-1/2`

---

## Chapter 13: Dynamic Classes with class: Directive

## What you learned:
- `class:name={condition}` for conditional classes
- Add classes dynamically based on props or state
- Much cleaner than React's template literals
- Combine static and dynamic classes easily

## React comparison:
```jsx
// React - Multiple approaches
// Approach 1: Template literals
<div className={`card ${highlighted ? 'highlighted' : ''}`}>

// Approach 2: ClassNames library
import classNames from 'classnames';
<div className={classNames('card', { highlighted })}>

// Approach 3: Conditional expression
<div className={highlighted ? 'card highlighted' : 'card'}>

// Svelte - Clean and simple
<div class="card" class:highlighted={highlighted}>
```

## Key differences:
- Much cleaner syntax than React's template literals
- No need for external libraries like classnames
- Readable and maintainable
- Works with both CSS classes and Tailwind utilities

## Multiple dynamic classes:
```svelte
// Svelte
<div
  class="base-class"
  class:active={isActive}
  class:disabled={isDisabled}
  class:highlighted={isHighlighted}
>
```

## When to use:
- Conditional styling based on props
- Dynamic state-based styling
- User interactions (hover, active, focus)
- Theme switching or mode changes