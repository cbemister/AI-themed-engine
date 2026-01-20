# Next.js Specific UI Improvement Prompt

## Context
You are improving UI designs specifically for Next.js applications, considering the framework's features, best practices, and modern React patterns.

## Next.js-Specific Considerations

### 1. Image Optimization
**AI-Generated Issue**: Using standard `<img>` tags or unoptimized images
**Solution**: Use Next.js Image component with proper sizing and loading strategies

```jsx
// ❌ AI-Generated Pattern
<img src="/hero.jpg" alt="Hero" />

// ✅ Professional Next.js
import Image from 'next/image'

<Image 
  src="/hero.jpg" 
  alt="Hero"
  width={1200}
  height={600}
  priority
  className="object-cover"
/>
```

### 2. Loading States & Suspense
**AI-Generated Issue**: No loading states or using generic spinners
**Solution**: Use Next.js 13+ loading.js and Suspense with skeleton screens

```jsx
// ❌ Generic Loading
{isLoading && <Spinner />}

// ✅ Professional Next.js
// app/dashboard/loading.js
export default function Loading() {
  return <DashboardSkeleton />
}
```

### 3. Layout Components
**AI-Generated Issue**: Duplicating navigation and footer across pages
**Solution**: Use layout.js files for shared UI elements

```jsx
// ✅ app/layout.js
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className="flex flex-col min-h-screen">
        <Navigation />
        <main className="flex-1">{children}</main>
        <Footer />
      </body>
    </html>
  )
}
```

### 4. Font Loading
**AI-Generated Issue**: Using web fonts without optimization, causing FOUT
**Solution**: Use Next.js font optimization

```jsx
// ✅ app/layout.js
import { Inter, Playfair_Display } from 'next/font/google'

const inter = Inter({ 
  subsets: ['latin'],
  variable: '--font-inter',
  display: 'swap'
})

const playfair = Playfair_Display({ 
  subsets: ['latin'],
  variable: '--font-playfair',
  display: 'swap'
})

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={`${inter.variable} ${playfair.variable}`}>
      <body className="font-sans">{children}</body>
    </html>
  )
}
```

### 5. Metadata & SEO
**AI-Generated Issue**: Missing or generic meta tags
**Solution**: Use Next.js metadata API

```jsx
// ✅ app/page.js
export const metadata = {
  title: 'Dashboard - Acme Corp',
  description: 'Manage your account and view analytics',
  openGraph: {
    title: 'Dashboard - Acme Corp',
    description: 'Manage your account and view analytics',
    images: ['/og-image.jpg'],
  },
}
```

### 6. Client vs Server Components
**AI-Generated Issue**: Making everything a client component unnecessarily
**Solution**: Use server components by default, client components only when needed

```jsx
// ✅ Server Component (default)
// app/blog/page.js
async function BlogPage() {
  const posts = await getPosts() // Fetches on server
  return <PostList posts={posts} />
}

// ✅ Client Component (when needed)
// components/SearchBar.js
'use client'
import { useState } from 'react'

export function SearchBar() {
  const [query, setQuery] = useState('')
  // Interactive component needs client
}
```

## Next.js UI Patterns to Implement

### 1. Skeleton Screens
Instead of spinners, show content-shaped loading states:

```jsx
// components/ui/skeleton.jsx
export function CardSkeleton() {
  return (
    <div className="animate-pulse space-y-4 p-6">
      <div className="h-4 bg-gray-200 rounded w-3/4"></div>
      <div className="h-4 bg-gray-200 rounded"></div>
      <div className="h-4 bg-gray-200 rounded w-5/6"></div>
    </div>
  )
}
```

### 2. Error Boundaries
Graceful error handling with error.js:

```jsx
// app/dashboard/error.js
'use client'

export default function Error({ error, reset }) {
  return (
    <div className="flex flex-col items-center justify-center min-h-[400px] space-y-4">
      <h2 className="text-xl font-semibold">Something went wrong</h2>
      <button 
        onClick={reset}
        className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition"
      >
        Try again
      </button>
    </div>
  )
}
```

### 3. Optimistic Updates
Show immediate feedback before server confirms:

```jsx
'use client'
import { useOptimistic } from 'react'

export function TodoList({ todos }) {
  const [optimisticTodos, addOptimisticTodo] = useOptimistic(
    todos,
    (state, newTodo) => [...state, { ...newTodo, pending: true }]
  )

  async function createTodo(formData) {
    addOptimisticTodo({ id: Date.now(), text: formData.get('text') })
    await saveTodo(formData)
  }

  return (
    <form action={createTodo}>
      {/* ... */}
    </form>
  )
}
```

### 4. Streaming with Suspense
Load parts of the page progressively:

```jsx
// app/dashboard/page.js
import { Suspense } from 'react'

export default function Dashboard() {
  return (
    <div className="space-y-8">
      <UserProfile />
      
      <Suspense fallback={<StatsSkeleton />}>
        <Stats />
      </Suspense>
      
      <Suspense fallback={<ActivitySkeleton />}>
        <RecentActivity />
      </Suspense>
    </div>
  )
}
```

## Performance Best Practices

### 1. Dynamic Imports
Load components only when needed:

```jsx
import dynamic from 'next/dynamic'

const Chart = dynamic(() => import('@/components/Chart'), {
  loading: () => <ChartSkeleton />,
  ssr: false // if component doesn't work on server
})
```

### 2. Route Prefetching
Next.js automatically prefetches links in viewport:

```jsx
// Prefetching is automatic for Link components
<Link href="/dashboard" prefetch={true}>
  Dashboard
</Link>
```

### 3. Parallel Routes
Load multiple sections simultaneously:

```jsx
// app/dashboard/@analytics/page.js
// app/dashboard/@activity/page.js
// app/dashboard/layout.js

export default function DashboardLayout({ analytics, activity }) {
  return (
    <div className="grid grid-cols-2 gap-8">
      <div>{analytics}</div>
      <div>{activity}</div>
    </div>
  )
}
```

## Common Next.js Anti-Patterns to Avoid

1. ❌ Not using the Image component
2. ❌ Ignoring loading and error states
3. ❌ Making everything a client component
4. ❌ Not optimizing fonts
5. ❌ Forgetting metadata for SEO
6. ❌ Using traditional page navigation without Link
7. ❌ Not leveraging server components for data fetching
8. ❌ Ignoring route prefetching benefits

## Improvement Checklist

- [ ] Replace `<img>` with Next.js `Image` component
- [ ] Add loading.js files for loading states
- [ ] Implement error.js for error handling
- [ ] Use layout.js for shared UI
- [ ] Optimize fonts with next/font
- [ ] Add proper metadata to all pages
- [ ] Use server components by default
- [ ] Implement Suspense for async components
- [ ] Add skeleton screens instead of spinners
- [ ] Use Link for all internal navigation
- [ ] Consider dynamic imports for large components
- [ ] Implement optimistic UI updates where appropriate
