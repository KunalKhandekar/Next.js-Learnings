# Data Fetching in Client component
    -> Runs in browser.
    -> Uses useEffect + useState.
    -> Fetch happens after page loads (not SEO friendly).
    -> Good for interactivity, live updates, private API calls.

# Data Fetching in Server component
    -> Runs on server.
    -> Fetch happens before sending HTML (good for SEO).
    -> Can use caching / ISR (revalidate).
    -> Faster initial load since data is embedded in HTML.

# Handling Loading 
    In Server Components, you don’t manage loading with useState, instead you rely on:
        -> loading.jsx (global per-route)
        -> <Suspense> (local section-level)

# Parallel API Calls

    🔴 Sequential (Slow)
    Fetch one after another → total time = sum of all requests.
    const posts = await getPosts();
    const users = await getUsers();

    🟢 Parallel with Promise.all
    Fetch all together → total time = longest request.
    const [posts, users] = await Promise.all([getPosts(), getUsers()]);

# Client Component Inside Server Component

    Some Confusion

# Using Context API
