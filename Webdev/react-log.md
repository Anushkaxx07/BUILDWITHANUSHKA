---

### 🗓️ July 19, 2025
- ✅ Today, I explored the basics of three essential React hooks: `useState`, `useEffect`, and `useRef`.

#### 🔹 `useState`
- Used to store and manage the state of a component.
- Updating the state with `setState` triggers a re-render to reflect the new value.

#### 🔹 `useEffect`
- Runs after the component renders or updates.
- Ideal for handling side effects like API calls, timers, logging, or any logic that depends on component lifecycle events.

#### 🔹 `useRef`
- Used to persist values across re-renders **without** causing re-renders.
- Helpful for storing mutable values and directly accessing DOM elements.
- Common use cases include:
  - Setting focus on input elements using `ref.current.focus()`
  - Storing and clearing timers (e.g., `setTimeout` or `setInterval`)

