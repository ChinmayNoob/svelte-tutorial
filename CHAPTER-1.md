# Chapter 1: Basic Counter with $state

## What you learned:
- `let count = $state(0);` creates reactive state
- When count changes, Svelte automatically updates the UI
- This is like React's `useState(0)` but simpler

## React comparison:
```jsx
// React
const [count, setCount] = useState(0);
setCount(count + 1);

// Svelte 5
let count = $state(0);
count++;
```

## Key difference:
No need for setter functions - direct reassignment works and triggers updates automatically.

---

# Chapter 2: Derived State with $derived and $derived.by

## What you learned:
- `let doubled = $derived(count * 2);` - simple expressions
- `let status = $derived.by(() => { ... });` - complex logic with multiple statements
- When dependencies change, derived values update automatically

## React comparison:
```jsx
// React
const doubled = useMemo(() => count * 2, [count]);
const status = useMemo(() => {
  if (count === 0) return 'Zero';
  if (count < 5) return 'Low';
  if (count < 10) return 'Medium';
  return 'High';
}, [count]);

// Svelte 5
let doubled = $derived(count * 2);
let status = $derived.by(() => {
  if (count === 0) return 'Zero';
  if (count < 5) return 'Low';
  if (count < 10) return 'Medium';
  return 'High';
});
```

## When to use which:
- `$derived(expr)` - for simple single expressions
- `$derived.by(() => { ... })` - for complex logic with if/else, multiple statements

---

# Chapter 3: Board Structure with Arrays

## What you learned:
- `let columns = $state([...])` creates reactive arrays
- `{#each columns as column (column.id)}...{/each}` renders lists efficiently
- Keys `(column.id)` help Svelte track items and update DOM correctly

## React comparison:
```jsx
// React
const columns = [
  { id: 1, title: 'Todo' },
  { id: 2, title: 'In Progress' },
  { id: 3, title: 'Done' }
];

{columns.map(column => (
  <div key={column.id}>
    <strong>{column.title}</strong> (ID: {column.id})
  </div>
))}

// Svelte 5
let columns = $state([
  { id: 1, title: 'Todo' },
  { id: 2, title: 'In Progress' },
  { id: 3, title: 'Done' }
]);

{#each columns as column (column.id)}
  <div>
    <strong>{column.title}</strong> (ID: {column.id})
  </div>
{/each}
```

## Key difference:
- Svelte's `{#each}` is more intuitive than `.map()`
- Keys are in parentheses: `(column.id)` instead of `key={column.id}`
- No need for wrapping function calls or return statements

---

# Chapter 4: Conditional Rendering with #if

## What you learned:
- `{#if condition}...{/if}` - basic conditional
- `{#if condition}...{:else if other}...{/if}` - multiple conditions
- `{#if condition}...{:else}...{/if}` - with fallback

## React comparison:
```jsx
// React
{count === 0 ? (
  <p>Status: Zero</p>
) : count < 5 ? (
  <p>Status: Low</p>
) : count < 10 ? (
  <p>Status: Medium</p>
) : (
  <p>Status: High</p>
)}

// Svelte 5
{#if count === 0}
  <p>Status: Zero</p>
{:else if count < 5}
  <p>Status: Low</p>
{:else if count < 10}
  <p>Status: Medium</p>
{:else}
  <p>Status: High</p>
{/if}
```

## Key difference:
- Svelte's template syntax is more readable than nested ternary operators
- Each condition block can contain multiple elements, not just a single expression
- No need for parentheses around the entire conditional expression

---

# Chapter 5: Side Effects with $effect

## What you learned:
- `$effect(() => { ... })` runs code when reactive dependencies change
- Automatically tracks which state variables are used
- Perfect for API calls, DOM manipulation, logging

## React comparison:
```jsx
// React
useEffect(() => {
  if (count > 0) {
    setLoading(true);
    fetch(`/api/todos/${count}`)
      .then(res => res.json())
      .then(json => {
        setData(json);
        setLoading(false);
      });
  }
}, [count]);

// Svelte 5
$effect(() => {
  if (count > 0) {
    loading = true;
    fetch(`/api/todos/${count}`)
      .then(res => res.json())
      .then(json => {
        data = json;
        loading = false;
      });
  }
});
```

## Key difference:
- No dependency array needed - Svelte automatically tracks dependencies
- Direct state assignment inside effect instead of setters
- Cleaner syntax without boilerplate

## Important notes:
- Effects run after DOM updates
- Use `$effect` for side effects, not for derived values
- Effects automatically clean up when component unmounts

---

# Chapter 6: Reactive Updates - Adding/Removing/Modifying Arrays

## What you learned:
- `columns = [...columns, newItem]` - add items to reactive arrays
- `columns = columns.filter(...)` - remove items from arrays
- `columns = columns.map(...)` - modify items in arrays
- Array immutability patterns work perfectly with Svelte

## React comparison:
```jsx
// React
const [columns, setColumns] = useState([...]);

function addColumn() {
  setColumns([...columns, { id: newId, title: 'New' }]);
}

function removeColumn(id) {
  setColumns(columns.filter(col => col.id !== id));
}

function updateColumn(id) {
  setColumns(columns.map(col =>
    col.id === id ? { ...col, cardCount: col.cardCount + 1 } : col
  ));
}

// Svelte 5
let columns = $state([...]);

function addColumn() {
  columns = [...columns, { id: newId, title: 'New' }];
}

function removeColumn(id) {
  columns = columns.filter(col => col.id !== id);
}

function updateColumn(id) {
  columns = columns.map(col =>
    col.id === id ? { ...col, cardCount: col.cardCount + 1 } : col
  );
}
```

## Key difference:
- No setter functions needed - direct reassignment triggers updates
- Same array immutability patterns you know from React
- Cleaner syntax without function calls for state updates