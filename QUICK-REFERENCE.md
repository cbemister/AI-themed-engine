# Quick Reference Guide

> Fast lookup for common AI-generated patterns and their fixes

## 🚨 Instant Red Flags

If you see these, your UI looks AI-generated:

| ❌ AI Pattern | ✅ Professional Fix |
|--------------|-------------------|
| `bg-blue-500` | `bg-blue-600` or `bg-indigo-600` |
| `px-4 py-2` everywhere | Vary: `px-3 py-1.5`, `px-6 py-2.5`, `px-8 py-3` |
| `rounded-lg` everywhere | Mix: `rounded-sm`, `rounded-md`, `rounded-xl`, `rounded-2xl` |
| `gap-4` everywhere | Vary: `gap-2`, `gap-6`, `gap-8`, `gap-12` |
| `text-2xl`, `text-lg`, `text-base` | Jump scales: `text-5xl`, `text-2xl`, `text-base`, `text-sm` |
| No hover states | Add `hover:bg-blue-700 hover:shadow-md transition-colors` |
| No focus states | Add `focus:ring-2 focus:ring-blue-500 focus:ring-offset-2` |
| `shadow` on everything | Use sparingly: `shadow-sm` + `hover:shadow-lg` |
| Grid cols-4 perfectly | Use cols-12 with spans: `col-span-7`, `col-span-5` |
| All centered | Left-align body text, center only headlines |

## 🎨 Color Quick Fixes

```jsx
// ❌ AI-Generated
bg-blue-500    → ✅ bg-blue-600 or bg-indigo-600
bg-green-500   → ✅ bg-emerald-600 or bg-green-700  
bg-red-500     → ✅ bg-red-600
bg-gray-500    → ✅ bg-slate-600 or bg-gray-700

// Background colors
bg-white       → ✅ bg-gray-50 (warmer, less harsh)
bg-gray-100    → ✅ bg-slate-50 (more sophisticated)
```

## 📏 Spacing Quick Fixes

```jsx
// ❌ Uniform spacing
<div className="p-4 space-y-4 gap-4">

// ✅ Intentional spacing  
<div className="p-6 space-y-8 gap-6">
  <header className="mb-12">
  <section className="py-24">
  <div className="mt-8">
```

**Spacing Scale**:
- Tight: 2, 3, 4 (8px-16px) - within components
- Medium: 6, 8, 12 (24px-48px) - between sections
- Loose: 16, 24, 32 (64px-128px) - major sections

## 🔤 Typography Quick Fixes

```jsx
// ❌ AI Pattern
<h1 className="text-2xl">Title</h1>
<p className="text-base">Body</p>

// ✅ Professional
<h1 className="text-5xl font-bold tracking-tight leading-tight">
  Title
</h1>
<p className="text-lg text-gray-700 leading-relaxed max-w-2xl">
  Body text with optimal line length
</p>
```

**Type Scale**:
- Hero: text-6xl, text-5xl (48px-60px)
- Headline: text-4xl, text-3xl (36px-48px)
- Subhead: text-2xl, text-xl (24px-30px)
- Body: text-lg, text-base (16px-18px)
- Small: text-sm, text-xs (12px-14px)

## 🎯 Button Quick Fix

```jsx
// ❌ AI-Generated
<button className="bg-blue-500 text-white px-4 py-2 rounded">
  Submit
</button>

// ✅ Professional
<button className="
  bg-blue-600 text-white px-6 py-2.5 rounded-lg font-medium
  hover:bg-blue-700 hover:shadow-md
  active:scale-[0.98]
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
  disabled:opacity-50 disabled:cursor-not-allowed
  transition-all duration-200
">
  Submit
</button>
```

## 🃏 Card Quick Fix

```jsx
// ❌ AI-Generated
<div className="bg-white p-4 rounded shadow">
  <h3>Title</h3>
  <p>Content</p>
</div>

// ✅ Professional
<div className="
  bg-white p-6 rounded-xl 
  border border-gray-100
  shadow-sm hover:shadow-lg
  transition-shadow duration-300
">
  <h3 className="text-xl font-semibold text-gray-900 mb-3">
    Title
  </h3>
  <p className="text-gray-600 leading-relaxed">
    Content with proper line height
  </p>
</div>
```

## 📝 Input Quick Fix

```jsx
// ❌ AI-Generated
<input type="text" placeholder="Email" className="border p-2 rounded" />

// ✅ Professional
<div className="space-y-2">
  <label htmlFor="email" className="block text-sm font-medium text-gray-700">
    Email address
  </label>
  <input 
    type="email"
    id="email"
    placeholder="you@example.com"
    className="
      w-full px-4 py-2.5 text-sm
      border border-gray-300 rounded-lg
      focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent
      hover:border-gray-400
      disabled:bg-gray-50 disabled:cursor-not-allowed
      transition-colors
    "
  />
</div>
```

## 🎭 State Quick Fixes

Every interactive element needs these states:

```jsx
// Complete state set
className="
  // Base
  bg-blue-600 text-white px-6 py-2.5 rounded-lg
  
  // Hover
  hover:bg-blue-700 hover:shadow-md
  
  // Active (pressed)
  active:scale-[0.98]
  
  // Focus (keyboard)
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
  
  // Disabled
  disabled:opacity-50 disabled:cursor-not-allowed
  
  // Transitions
  transition-all duration-200
"
```

## 🏗️ Layout Quick Fix

```jsx
// ❌ AI Pattern - Perfect symmetry
<div className="grid grid-cols-3 gap-4">
  <Card />
  <Card />
  <Card />
</div>

// ✅ Professional - Asymmetric
<div className="grid grid-cols-12 gap-6">
  <div className="col-span-7">
    <FeaturedCard />
  </div>
  <div className="col-span-5 space-y-6">
    <Card />
    <Card />
  </div>
</div>
```

## ⚡ Next.js Quick Fixes

```jsx
// ❌ Standard img tag
<img src="/hero.jpg" alt="Hero" />

// ✅ Next.js Image
import Image from 'next/image'
<Image src="/hero.jpg" alt="Hero" width={1200} height={600} priority />

// ❌ No loading state
export default function Page() { /* ... */ }

// ✅ Loading state
// app/page/loading.js
export default function Loading() {
  return <Skeleton />
}

// ❌ Generic fonts
<div className="font-sans">

// ✅ Optimized fonts
import { Inter } from 'next/font/google'
const inter = Inter({ subsets: ['latin'] })
<div className={inter.className}>
```

## ♿ Accessibility Quick Fixes

```jsx
// ❌ Icon button without label
<button><XIcon /></button>

// ✅ With accessible label
<button aria-label="Close dialog">
  <XIcon aria-hidden="true" />
</button>

// ❌ Div as button
<div onClick={handleClick}>Click me</div>

// ✅ Proper button
<button onClick={handleClick}>Click me</button>

// ❌ No focus indicator
<button className="outline-none">

// ✅ Visible focus
<button className="focus:outline-none focus:ring-2 focus:ring-blue-500">
```

## 🎬 Animation Quick Add

```jsx
// Add to any interactive element
className="
  transition-all duration-200
  hover:scale-105 hover:shadow-md
  active:scale-95
"

// For entering elements
className="
  animate-in fade-in slide-in-from-bottom-4 duration-500
"

// For smooth color changes
className="
  transition-colors duration-200
"
```

## 📊 Common Mistakes Checklist

Before calling it done, check:

- [ ] Varied spacing (not all p-4, gap-4)
- [ ] Deeper colors (not blue-500)
- [ ] Complete states (hover, focus, active, disabled)
- [ ] Visible focus indicators
- [ ] Proper typography hierarchy (dramatic size jumps)
- [ ] Asymmetric layout (not all equal columns)
- [ ] Transitions (200-300ms)
- [ ] Alt text on images
- [ ] Labels on inputs
- [ ] Loading states (skeleton screens)
- [ ] Error states for forms
- [ ] Max-width on body text (max-w-2xl)
- [ ] Line height (leading-relaxed for body)
- [ ] Font weights (use 400, 600, 700)
- [ ] WCAG contrast (4.5:1 minimum)

## 🚀 Quick Start Templates

### Professional Button Set
```jsx
// Primary
<button className="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2.5 rounded-lg font-medium shadow-sm hover:shadow-md active:scale-[0.98] focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-all duration-200">
  Primary
</button>

// Secondary
<button className="bg-white hover:bg-gray-50 text-gray-700 border border-gray-300 hover:border-gray-400 px-6 py-2.5 rounded-lg font-medium shadow-sm active:scale-[0.98] focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-all duration-200">
  Secondary
</button>

// Ghost
<button className="bg-transparent hover:bg-blue-50 text-blue-600 px-4 py-2 rounded-lg font-medium active:bg-blue-100 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-colors duration-200">
  Ghost
</button>
```

### Professional Card
```jsx
<div className="bg-white rounded-xl border border-gray-100 p-6 shadow-sm hover:shadow-lg transition-shadow duration-300 group">
  <div className="flex items-start justify-between mb-4">
    <h3 className="text-xl font-semibold text-gray-900">Card Title</h3>
    <span className="px-2.5 py-1 text-xs font-medium rounded-full bg-blue-50 text-blue-700">New</span>
  </div>
  <p className="text-gray-600 leading-relaxed mb-6">
    Card content with proper spacing and typography
  </p>
  <button className="text-sm font-medium text-blue-600 hover:text-blue-700 transition-colors inline-flex items-center gap-2 group-hover:translate-x-1 transition-transform">
    Learn more →
  </button>
</div>
```

## 💡 Remember

**Good design is intentional.** Every choice should have a reason:
- **Why this color?** → Deeper tones feel professional
- **Why this spacing?** → Creates hierarchy and rhythm
- **Why this animation?** → Provides user feedback
- **Why this layout?** → Emphasizes important content

If you can't explain why, you're probably following AI patterns.

---

## 📚 Full Documentation

For detailed explanations, see:
- [`docs/theme-engine-guide.md`](docs/theme-engine-guide.md) - Complete guide
- [`docs/design-principles.md`](docs/design-principles.md) - Why things work
- [`docs/anti-patterns.md`](docs/anti-patterns.md) - What to avoid
- [`prompts/ui-improvement-master.md`](prompts/ui-improvement-master.md) - Use with Claude

---

**Last updated**: 2024
**Status**: Production ready 🚀
