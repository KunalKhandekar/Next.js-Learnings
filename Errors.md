# Errors in Next.js

1. Basic Route level Error handling using error.jsx
2. Recover from error: 
    -> You can recover without full page reload using the reset() function in error.js.
    -> And for server component use startTransition() and router.refresh()
3. Error handling in nested route:
    -> Each route segment can have its own error.js.
    -> Errors bubble up only within that route boundary.
4. Client-Side Exception:
    It is an error that happens after the page has been loaded and rendered in the browser — typically caused by JavaScript issues like:
    (1) Accessing undefined variables
    (2) Bad useEffect logic
    (3) Component crashes (e.g., null.map(...))
    (4) API fetch failures (only when triggered in client components)
4. Global Error Handling in Next.js
    For handling the error in the root layout we must create a global-error.jsx
    This only catches error in production mode.
    It must return a <html></html>.
