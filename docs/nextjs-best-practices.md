# Next.js Best Practices for Professional UIs

## Introduction

This guide covers Next.js-specific best practices for creating professional, performant UIs that don't look AI-generated. It focuses on leveraging Next.js features effectively.

## App Router (Next.js 13+) Best Practices

### 1. Server Components by Default

**Principle**: Use Server Components unless you need client-side interactivity.

**Benefits**:
- Smaller JavaScript bundle
- Faster initial load
- Better SEO
- Automatic code splitting

```jsx
// ✅ Server Component (default)
// app/blog/page.js
import { getPosts } from '@/lib/posts'

export default async function BlogPage() {
  const posts = await getPosts() // Runs on server
  
  return (
    <div className="max-w-4xl mx-auto py-12">
      <h1 className="text-4xl font-bold mb-8">Blog</h1>
      <div className="space-y-6">
        {posts.map(post => (
          <BlogCard key={post.id} post={post} />
        ))}
      </div>
    </div>
  )
}

// ✅ Client Component (only when needed)
// components/SearchBar.js
'use client'
import { useState } from 'react'

export function SearchBar() {
  const [query, setQuery] = useState('')
  
  return (
    <input 
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      className="..."
    />
  )
}
```

**When to Use Client Components**:
- useState, useEffect, or other React hooks
- Event listeners (onClick, onChange, etc.)
- Browser APIs (localStorage, window, etc.)
- Third-party libraries that use browser features

---

### 2. Parallel Data Fetching

**Principle**: Fetch data in parallel rather than sequentially for better performance.

```jsx
// ❌ Sequential fetching (slower)
async function Page() {
  const user = await getUser()
  const posts = await getPosts(user.id)
  const comments = await getComments(user.id)
  
  return <Dashboard user={user} posts={posts} comments={comments} />
}

// ✅ Parallel fetching (faster)
async function Page() {
  const [user, posts, comments] = await Promise.all([
    getUser(),
    getPosts(),
    getComments()
  ])
  
  return <Dashboard user={user} posts={posts} comments={comments} />
}
```

---

### 3. Streaming with Suspense

**Principle**: Stream content as it becomes available instead of waiting for everything.

```jsx
// ✅ Stream content progressively
// app/dashboard/page.js
import { Suspense } from 'react'

export default function Dashboard() {
  return (
    <div className="space-y-8 p-6">
      {/* Shows immediately */}
      <Header />
      
      {/* Streams when ready */}
      <Suspense fallback={<UserProfileSkeleton />}>
        <UserProfile />
      </Suspense>
      
      <div className="grid grid-cols-2 gap-6">
        <Suspense fallback={<StatsSkeleton />}>
          <Stats />
        </Suspense>
        
        <Suspense fallback={<ActivitySkeleton />}>
          <RecentActivity />
        </Suspense>
      </div>
    </div>
  )
}

// Stats component fetches its own data
async function Stats() {
  const stats = await getStats() // Can be slow
  return <StatsDisplay stats={stats} />
}
```

---

### 4. Professional Loading States

**Principle**: Use skeleton screens instead of spinners for better UX.

```jsx
// ✅ app/dashboard/loading.js
export default function Loading() {
  return (
    <div className="space-y-8 p-6">
      {/* Skeleton matches actual layout */}
      <div className="flex items-center gap-4">
        <div className="w-16 h-16 bg-gray-200 rounded-full animate-pulse" />
        <div className="space-y-2">
          <div className="h-6 bg-gray-200 rounded w-40 animate-pulse" />
          <div className="h-4 bg-gray-200 rounded w-32 animate-pulse" />
        </div>
      </div>
      
      <div className="grid grid-cols-2 gap-6">
        <CardSkeleton />
        <CardSkeleton />
      </div>
    </div>
  )
}

// Reusable skeleton component
function CardSkeleton() {
  return (
    <div className="bg-white rounded-xl border border-gray-200 p-6 space-y-4">
      <div className="h-8 bg-gray-200 rounded w-3/4 animate-pulse" />
      <div className="space-y-2">
        <div className="h-4 bg-gray-200 rounded animate-pulse" />
        <div className="h-4 bg-gray-200 rounded w-5/6 animate-pulse" />
      </div>
    </div>
  )
}
```

---

### 5. Error Handling with error.js

**Principle**: Provide helpful error states instead of crashing.

```jsx
// ✅ app/dashboard/error.js
'use client'

export default function Error({ error, reset }) {
  return (
    <div className="flex flex-col items-center justify-center min-h-[400px] px-4">
      <div className="text-center space-y-4 max-w-md">
        <div className="w-16 h-16 bg-red-100 rounded-full flex items-center justify-center mx-auto">
          <svg className="w-8 h-8 text-red-600" /* error icon */ />
        </div>
        
        <h2 className="text-2xl font-semibold text-gray-900">
          Something went wrong
        </h2>
        
        <p className="text-gray-600">
          We encountered an error loading your dashboard. 
          Please try again or contact support if the problem persists.
        </p>
        
        <div className="flex gap-3 justify-center">
          <button 
            onClick={reset}
            className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition"
          >
            Try again
          </button>
          
          <a 
            href="/support"
            className="px-4 py-2 bg-white border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition"
          >
            Contact support
          </a>
        </div>
      </div>
    </div>
  )
}
```

---

### 6. Metadata and SEO

**Principle**: Use Next.js metadata API for proper SEO.

```jsx
// ✅ Static metadata
// app/page.js
export const metadata = {
  title: 'Acme Corp - Ship Better Products Faster',
  description: 'Join 10,000+ teams using Acme to reduce development time by 40%',
  openGraph: {
    title: 'Acme Corp - Ship Better Products Faster',
    description: 'Join 10,000+ teams using Acme to reduce development time by 40%',
    images: [
      {
        url: '/og-image.jpg',
        width: 1200,
        height: 630,
        alt: 'Acme Corp Dashboard'
      }
    ],
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Acme Corp - Ship Better Products Faster',
    description: 'Join 10,000+ teams using Acme to reduce development time by 40%',
    images: ['/og-image.jpg'],
  },
}

// ✅ Dynamic metadata
// app/blog/[slug]/page.js
export async function generateMetadata({ params }) {
  const post = await getPost(params.slug)
  
  return {
    title: `${post.title} | Acme Blog`,
    description: post.excerpt,
    openGraph: {
      title: post.title,
      description: post.excerpt,
      images: [post.coverImage],
      type: 'article',
      publishedTime: post.publishedAt,
      authors: [post.author.name],
    },
  }
}
```

---

### 7. Image Optimization

**Principle**: Always use Next.js Image component for automatic optimization.

```jsx
import Image from 'next/image'

// ✅ Hero image with priority
export function Hero() {
  return (
    <div className="relative h-[600px] w-full">
      <Image
        src="/hero.jpg"
        alt="Professional workspace with modern design"
        fill
        priority // Load immediately
        className="object-cover"
        sizes="100vw"
      />
      
      <div className="relative z-10 flex items-center justify-center h-full">
        <h1 className="text-5xl font-bold text-white">Welcome</h1>
      </div>
    </div>
  )
}

// ✅ Gallery images with lazy loading
export function Gallery({ images }) {
  return (
    <div className="grid grid-cols-3 gap-4">
      {images.map((image) => (
        <div key={image.id} className="relative aspect-square">
          <Image
            src={image.url}
            alt={image.alt}
            fill
            className="object-cover rounded-lg"
            sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
          />
        </div>
      ))}
    </div>
  )
}

// ✅ Avatar with fixed dimensions
export function Avatar({ src, alt }) {
  return (
    <div className="relative w-12 h-12">
      <Image
        src={src}
        alt={alt}
        width={48}
        height={48}
        className="rounded-full object-cover"
      />
    </div>
  )
}
```

---

### 8. Font Optimization

**Principle**: Use next/font for automatic font optimization.

```jsx
// ✅ app/layout.js
import { Inter, Playfair_Display } from 'next/font/google'

const inter = Inter({ 
  subsets: ['latin'],
  variable: '--font-inter',
  display: 'swap', // Prevent FOUT
})

const playfair = Playfair_Display({ 
  subsets: ['latin'],
  variable: '--font-playfair',
  display: 'swap',
  weight: ['400', '700'],
})

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={`${inter.variable} ${playfair.variable}`}>
      <body className="font-sans antialiased">{children}</body>
    </html>
  )
}

// Use in tailwind.config.js
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        sans: ['var(--font-inter)'],
        serif: ['var(--font-playfair)'],
      },
    },
  },
}

// ✅ Local fonts
import localFont from 'next/font/local'

const customFont = localFont({
  src: [
    {
      path: './fonts/CustomFont-Regular.woff2',
      weight: '400',
      style: 'normal',
    },
    {
      path: './fonts/CustomFont-Bold.woff2',
      weight: '700',
      style: 'normal',
    },
  ],
  variable: '--font-custom',
})
```

---

### 9. Route Groups and Layouts

**Principle**: Use route groups for shared layouts without affecting URLs.

```jsx
// Directory structure
// app/
//   (marketing)/
//     layout.js      ← Marketing layout
//     page.js        ← /
//     about/
//       page.js      ← /about
//   (dashboard)/
//     layout.js      ← Dashboard layout
//     dashboard/
//       page.js      ← /dashboard
//     settings/
//       page.js      ← /settings

// ✅ app/(marketing)/layout.js
export default function MarketingLayout({ children }) {
  return (
    <>
      <MarketingNav />
      <main className="min-h-screen">{children}</main>
      <MarketingFooter />
    </>
  )
}

// ✅ app/(dashboard)/layout.js
export default function DashboardLayout({ children }) {
  return (
    <div className="flex h-screen">
      <Sidebar />
      <main className="flex-1 overflow-auto p-6">
        {children}
      </main>
    </div>
  )
}
```

---

### 10. Dynamic Imports

**Principle**: Code-split large components that aren't immediately needed.

```jsx
import dynamic from 'next/dynamic'

// ✅ Dynamic import with loading state
const Chart = dynamic(() => import('@/components/Chart'), {
  loading: () => (
    <div className="h-64 flex items-center justify-center">
      <div className="animate-pulse text-gray-400">Loading chart...</div>
    </div>
  ),
  ssr: false, // Don't render on server if it uses browser APIs
})

// ✅ Dynamic import for modals
const Modal = dynamic(() => import('@/components/Modal'))

export function Page() {
  const [isOpen, setIsOpen] = useState(false)
  
  return (
    <div>
      <button onClick={() => setIsOpen(true)}>Open Modal</button>
      {isOpen && <Modal onClose={() => setIsOpen(false)} />}
    </div>
  )
}
```

---

### 11. Server Actions

**Principle**: Use Server Actions for form submissions and mutations.

```jsx
// ✅ app/actions.js
'use server'

import { revalidatePath } from 'next/cache'

export async function createPost(formData) {
  const title = formData.get('title')
  const content = formData.get('content')
  
  // Validate
  if (!title || !content) {
    return { error: 'Title and content are required' }
  }
  
  // Save to database
  await db.posts.create({ title, content })
  
  // Revalidate cache
  revalidatePath('/blog')
  
  return { success: true }
}

// ✅ Form component
import { createPost } from './actions'

export function CreatePostForm() {
  return (
    <form action={createPost} className="space-y-4">
      <div>
        <label htmlFor="title" className="block text-sm font-medium mb-2">
          Title
        </label>
        <input 
          type="text"
          id="title"
          name="title"
          required
          className="w-full px-4 py-2 border rounded-lg"
        />
      </div>
      
      <div>
        <label htmlFor="content" className="block text-sm font-medium mb-2">
          Content
        </label>
        <textarea 
          id="content"
          name="content"
          required
          rows={6}
          className="w-full px-4 py-2 border rounded-lg"
        />
      </div>
      
      <button 
        type="submit"
        className="px-6 py-2.5 bg-blue-600 text-white rounded-lg hover:bg-blue-700"
      >
        Create Post
      </button>
    </form>
  )
}
```

---

### 12. Optimistic UI Updates

**Principle**: Show immediate feedback before server confirms.

```jsx
'use client'
import { useOptimistic } from 'react'
import { toggleTodo } from './actions'

export function TodoList({ todos }) {
  const [optimisticTodos, addOptimisticTodo] = useOptimistic(
    todos,
    (state, { id, completed }) => 
      state.map(todo => 
        todo.id === id ? { ...todo, completed } : todo
      )
  )

  async function handleToggle(id, completed) {
    // Update UI immediately
    addOptimisticTodo({ id, completed: !completed })
    
    // Then update server
    await toggleTodo(id)
  }

  return (
    <ul className="space-y-2">
      {optimisticTodos.map(todo => (
        <li 
          key={todo.id}
          className={todo.pending ? 'opacity-50' : ''}
        >
          <label className="flex items-center gap-3 p-3 hover:bg-gray-50 rounded-lg cursor-pointer">
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => handleToggle(todo.id, todo.completed)}
              className="w-5 h-5 rounded border-gray-300"
            />
            <span className={todo.completed ? 'line-through text-gray-500' : ''}>
              {todo.text}
            </span>
          </label>
        </li>
      ))}
    </ul>
  )
}
```

---

## Performance Best Practices

### 1. Preload Critical Resources

```jsx
// app/layout.js
export default function RootLayout({ children }) {
  return (
    <html>
      <head>
        <link 
          rel="preload" 
          href="/fonts/custom-font.woff2" 
          as="font" 
          type="font/woff2" 
          crossOrigin="anonymous" 
        />
      </head>
      <body>{children}</body>
    </html>
  )
}
```

### 2. Static Generation When Possible

```jsx
// ✅ Generate static pages at build time
export async function generateStaticParams() {
  const posts = await getPosts()
  
  return posts.map((post) => ({
    slug: post.slug,
  }))
}

export default async function Post({ params }) {
  const post = await getPost(params.slug)
  return <PostContent post={post} />
}
```

### 3. Incremental Static Regeneration

```jsx
// Revalidate every hour
export const revalidate = 3600

export default async function Page() {
  const data = await fetchData()
  return <Content data={data} />
}
```

---

## Accessibility in Next.js

### 1. Proper HTML Structure

```jsx
// ✅ Semantic HTML
export default function Page() {
  return (
    <>
      <header>
        <nav>
          <Link href="/">Home</Link>
        </nav>
      </header>
      
      <main>
        <article>
          <h1>Page Title</h1>
          <p>Content</p>
        </article>
      </main>
      
      <footer>
        <p>&copy; 2024 Acme Corp</p>
      </footer>
    </>
  )
}
```

### 2. Focus Management

```jsx
'use client'
import { useEffect, useRef } from 'react'
import { usePathname } from 'next/navigation'

export function FocusManagement() {
  const pathname = usePathname()
  const mainRef = useRef(null)
  
  useEffect(() => {
    // Focus main content on route change
    mainRef.current?.focus()
  }, [pathname])
  
  return (
    <main ref={mainRef} tabIndex={-1} className="outline-none">
      {/* Content */}
    </main>
  )
}
```

---

## Conclusion

Professional Next.js applications leverage framework features to create fast, accessible, well-structured UIs. The key is understanding and using:

1. Server Components for performance
2. Streaming for better UX
3. Proper metadata for SEO
4. Image and font optimization
5. Error and loading states
6. Accessibility features

By following these practices, your Next.js applications will not only look professional but also perform excellently.
