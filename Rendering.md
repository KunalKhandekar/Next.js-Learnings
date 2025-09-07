# Rendering Strategies
    Docs: https://nextjs.org/learn/seo/rendering-strategies

# ⚡ Static vs Dynamic Rendering in App Router

    Static Rendering (Default in App Router)
        -> By default, all components in the App Router are statically rendered.
        -> Next.js pre-renders them at build time (SSG) or caches them at the edge/CDN.
        -> Static rendering happens once and the same HTML is served to all users.

        -> Example:
            // app/page.tsx
            export default function Home() {
            return <h1>Hello, this is statically rendered!</h1>
            }


    Dynamic Rendering
        -> If your page depends on per-request data (cookies, headers, DB queries, real-time APIs), Next.js switches to Dynamic Rendering.
        -> This happens at request time on the server.

        -> Example:
            // app/dashboard/page.tsx
            import { cookies } from "next/headers";

            export default function Dashboard() {
            const cookieStore = cookies();
            const user = cookieStore.get("user");

            return <h1>Welcome back, {user?.value || "Guest"}!</h1>;
            }

# ⚡ What is SSG?

    Static Site Generation (SSG) means your pages are pre-rendered at build time into static HTML files. These files are then served to users directly from the CDN or server without extra computation.
        -> Faster page load (HTML already ready).
        -> SEO-friendly.
        -> Great for content that doesn’t change often.

    ⚡ How SSG works in the App Router
        In the App Router (app/ directory introduced in Next.js 13), SSG happens by default when:
            -> Your page doesn’t use dynamic data (fetch, database, etc.).
            -> Or when you fetch data using fetch() with { cache: 'force-cache' } (default behavior).
            -> Or when you use generateStaticParams in dynamic routes.
    
# Dynamic Params

    -> dynamicParams = true → allow extra paths not in generateStaticParams (fallback: dynamic rendering).
    -> dynamicParams = false → only pre-rendered paths are valid, others show 404.
    -> Default is true.

# What is ISR?

    -> ISR = Incremental Static Regeneration
    -> It allows you to update static pages after the site is built, without rebuilding the whole app.
    -> Pages are generated at build time (like SSG).
    -> After a configured time (revalidate), Next.js regenerates the page in the background.
    -> Users get updated content without full redeploys.
    -> So, you get the speed of SSG + freshness of SSR.

    ISR in App Router
        -> In the App Router (app/), ISR is controlled with the revalidate export.
        -> export const revalidate = <number | false>;
            number → time in seconds after which the page should be regenerated.
            false → disable revalidation (pure static).
            0 → always fetch fresh data (like SSR).
        
# Dynamically rendering static pages

    -> Dynamically rendering static pages = controlling when static pages should be re-generated or bypassed dynamically.
    -> In Next.js App Router, you can choose:
        Pure static (SSG) → force-static / default.
        Dynamic rendering → force-dynamic or cache: "no-store".
        Hybrid (ISR) → revalidate for periodic regeneration.

# Streaming in Next.js

    What is Streaming?
        -> Normally, when you render a React/Next.js page:
        -> The server waits for all data fetching to finish.
        -> Then it sends the complete HTML to the browser.
        -> This can cause longer loading times, especially if one slow API blocks the whole page.

    Streaming solves this by:
        -> Breaking the page into chunks (React Server Components).
        -> Sending ready parts of the UI immediately.
        -> Filling in the rest as data arrives.
        -> So, users see content faster.

    Streaming in Next.js App Router

    -> In the App Router, streaming is enabled by default.
    -> It uses two main tools:

        1. <Suspense>
            -> Wrap parts of your UI that depend on slow data.
            -> Show a fallback while waiting.
            -> Stream results later.
        
        2. loading.tsx (Route-level Suspense)
            -> Each route in App Router can have a loading.tsx/.jsx file.
            -> It automatically becomes the fallback for that route while data loads.

# Client Vs Server Component

    Server Components
        -> Default in Next.js App Router → Every component is a server component unless you explicitly mark it as client.
        -> Runs only on the server, never shipped to the browser.
        -> Can fetch data directly from databases or APIs (no need for API routes).
        -> Smaller bundle size since code is not sent to the client.
        -> Cannot use React hooks like useState, useEffect, or browser APIs (e.g., localStorage, window).
        -> Great for data-heavy, static, or cached UI.

    Client Components
        -> Declared with "use client" at the top of the file.
        -> Runs on the browser → bundled and shipped to the client.
        -> Can use React hooks (useState, useEffect, useContext), event listeners, and browser APIs.
        -> Cannot directly access backend resources (databases, private APIs). Need API routes or server actions.
        -> Best for interactive UI (buttons, forms, dropdowns, modals).

# Hydration

    Hydration is the process where the JavaScript code on the client (browser) takes over the already-rendered HTML from the server, making it interactive.

    Think of it like:
        -> Server sends a static HTML page → fast to load, SEO-friendly.
        -> Browser downloads the React JavaScript bundle.
        -> React “hydrates” the HTML by attaching event listeners (onClick, onChange, etc.) and enabling hooks (useState, useEffect).
        -> Now the page becomes interactive.

    Without Hydration (just server-rendered HTML):
        -> User sees content quickly.
        -> But buttons, forms, dropdowns → won’t work.

    With Hydration:
        -> User sees content and can interact.

# Hydration error 

    -> A hydration error happens when the HTML generated on the server does not match the HTML React expects on the client during hydration.
    -> Basically, React tries to “attach” its virtual DOM to the server-rendered HTML, but if there’s a mismatch → ⚠️ hydration error.

    Common Causes of Hydration Errors in Next.js / React:
        1. Different HTML on server vs client
        2. Accessing Browser APIs in Server Components
        3. Conditional Rendering Differences
        4. Async Data Fetching Issues
        5. Mismatched Attributes

    How to Fix Hydration Errors:
        -> Avoid non-deterministic values in render (Math.random(), Date.now()).
        -> Use "use client" only when necessary.
        -> If something must run only on client, wrap it in useEffect.
        -> Use suppressHydrationWarning if mismatch is intentional:
            <p suppressHydrationWarning>{new Date().toString()}</p>
