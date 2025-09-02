# Intro to Next.js

## ⚡ What is Next.js?

    Next.js is a React framework created by Vercel. It helps developers build full-stack, production-ready, SEO-friendly web applications with features like server rendering, static generation, API routes, and optimizations built-in.

    ⚡ Key Features:
        File-based Routing
            -> Routes are defined by folder/file structure.
            -> Example: app/about/page.tsx → /about

        Two Routers
            -> App Router (/app) → Modern, based on React Server Components (recommended).
            -> Pages Router (/pages) → Legacy, uses getServerSideProps & getStaticProps.

        Rendering Options
            -> SSR (Server-Side Rendering): fresh HTML per request.
            -> SSG (Static Site Generation): prebuilt at build time.
            -> ISR (Incremental Static Regeneration): revalidate cached pages automatically.
            -> Streaming & Suspense: load parts of the UI progressively.

        Data Fetching
            -> Server components can fetch directly (secure, no client bundle).
            -> fetch supports caching, revalidation, and deduplication.
            -> Client components ("use client") handle interactivity.

        API Routes / Route Handlers
            -> You can build backend endpoints in /app/api/* or /pages/api/*.
            -> Example: /app/api/posts/route.ts handles GET/POST for /api/posts.

        Server Actions
            -> "use server" functions to mutate data directly from forms or client components.
            -> Eliminates the need for extra API calls in many cases.

        Optimizations
            -> Automatic code splitting & prefetching.
            -> <Image /> → optimized, lazy-loaded images.
            -> <Link /> → fast client-side transitions.
            -> next/font → built-in font optimization.

        Middleware & Edge
            -> Run logic (auth, rewrites, A/B tests) on every request with middleware.ts.
            -> Deploy functions close to users for low latency.

        Deployment
            -> First-class support on Vercel (zero-config).
            -> Can also run on Node.js servers, Docker, or other cloud providers.

    ⚡ Benefits of Next.js
        -> SEO-friendly (server rendering, static HTML).
        -> Full-stack (frontend + backend in one project).
        -> Performance (code splitting, caching, streaming).
        -> Developer experience (file-based routing, TypeScript, fast dev server).
        -> Scales well (from blogs to enterprise apps).

    ⚡ When NOT to use Next.js
        -> If you’re building a pure SPA (no SEO needs, only client rendering).
        -> If you need a very custom build setup without conventions.

## Steps to Create a Next.js App

    1. Prerequisites
        -> Make sure you have:
            Node.js (version 18+ recommended)
            npm (comes with Node)

        -> Check versions:
            node -v
            npm -v

    2. Create a New Next.js Project
        -> Run this in your terminal:
            npx create-next-app@latest my-first-app

        -> It will ask a few questions:
            TypeScript? 
            ESLint?
            Tailwind CSS? 
            App Router? 
            Import alias? 
        -> This creates a folder my-first-app with all boilerplate files.

    3. Start the Development Server
        -> Go inside the project and run:
            cd my-first-app
            npm run dev
        -> Now open http://localhost:3000 in your browser.
        -> You should see the Next.js welcome page.

## 📌 React.js vs Next.js

React.js
    -> A JavaScript library for building UI components.
    -> Handles only the view layer of an app (frontend).
    -> Uses client-side rendering (CSR) by default.
    -> Requires extra tools (e.g., React Router, Redux, Webpack, Vite) for routing, state management, and optimizations.
    -> SEO is harder because pages render on the client.
    -> Great for single-page applications (SPAs).

Next.js
    -> A full-stack React framework built on top of React.
    -> Provides file-based routing out of the box.
    -> Supports multiple rendering modes: SSR, SSG, ISR, CSR.
    -> Has built-in features: API routes, Image optimization, Fonts, Middleware, Edge runtime.
    -> SEO-friendly due to server-side and static rendering.
    -> Great for production-ready apps like blogs, e-commerce, and SaaS.