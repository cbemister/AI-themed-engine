# Anti-Patterns: What Makes UIs Look AI-Generated

## Introduction

This document catalogs common patterns that make UI designs obviously AI-generated. Learning to recognize and avoid these patterns is crucial for creating professional interfaces.

## Visual Anti-Patterns

### 1. The "Perfect Grid" Syndrome

**Problem**: AI loves perfectly uniform grids with identical spacing and sizing.

```jsx
// ❌ AI Pattern - Too perfect
<div className="grid grid-cols-4 gap-4 p-4">
  <Card height="200px" />
  <Card height="200px" />
  <Card height="200px" />
  <Card height="200px" />
</div>
```

**Why It Looks AI-Generated**:
- Every element is exactly the same size
- Spacing is perfectly uniform
- No visual hierarchy or focal point
- Feels mechanical and lifeless

**Professional Alternative**:
```jsx
// ✅ Professional - Intentional variety
<div className="grid grid-cols-12 gap-6 p-6">
  <div className="col-span-7 row-span-2">
    <FeaturedCard className="h-full" />
  </div>
  <div className="col-span-5">
    <Card />
  </div>
  <div className="col-span-5">
    <Card />
  </div>
  <div className="col-span-12">
    <WideCard />
  </div>
</div>
```

---

### 2. The "Blue Button" Cliché

**Problem**: Default to `bg-blue-500` for primary actions without consideration.

```jsx
// ❌ AI Pattern
<button className="bg-blue-500 text-white px-4 py-2 rounded">
  Submit
</button>
```

**Why It Looks AI-Generated**:
- `#3B82F6` (blue-500) is the most generic choice
- No consideration for brand or context
- Often paired with `bg-green-500` for success
- Oversaturated and web 2.0-feeling

**Professional Alternatives**:
```jsx
// ✅ Deeper, more sophisticated blue
<button className="bg-blue-600 hover:bg-blue-700">
  Submit
</button>

// ✅ Indigo for modern feel
<button className="bg-indigo-600 hover:bg-indigo-700">
  Submit
</button>

// ✅ Custom brand color
<button className="bg-[#2D5BFF] hover:bg-[#1E4FE5]">
  Submit
</button>

// ✅ Gradient (when appropriate)
<button className="bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-700 hover:to-indigo-700">
  Submit
</button>
```

---

### 3. The "Everything is Rounded-lg" Pattern

**Problem**: Apply `rounded-lg` to every single element.

```jsx
// ❌ AI Pattern - Same radius everywhere
<div className="rounded-lg">
  <img className="rounded-lg" />
  <button className="rounded-lg">Click</button>
  <input className="rounded-lg" />
</div>
```

**Why It Looks AI-Generated**:
- No variation in border radius
- Doesn't consider element purpose or hierarchy
- Makes everything blend together

**Professional Approach**:
```jsx
// ✅ Varied border radius with purpose
<div className="rounded-2xl overflow-hidden">
  <img className="rounded-t-2xl" />
  <div className="p-6">
    <button className="rounded-lg">Click</button>
    <input className="rounded-md" />
  </div>
</div>
```

**Border Radius Guide**:
- `rounded-sm` (2px): Subtle, for small elements
- `rounded` or `rounded-md` (4-6px): Inputs, small buttons
- `rounded-lg` (8px): Cards, medium buttons
- `rounded-xl` (12px): Large cards, feature sections
- `rounded-2xl` (16px): Hero sections, modals
- `rounded-full`: Pills, avatars, icon buttons

---

### 4. Uniform Spacing Everywhere

**Problem**: Using the same spacing value throughout (usually `p-4` or `gap-4`).

```jsx
// ❌ AI Pattern
<section className="p-4">
  <h1 className="mb-4">Title</h1>
  <div className="space-y-4">
    <p className="mb-4">Content</p>
    <button className="mt-4">Action</button>
  </div>
</section>
```

**Why It Looks AI-Generated**:
- No rhythm or visual interest
- Doesn't create hierarchy
- Everything feels equally important (or unimportant)

**Professional Spacing**:
```jsx
// ✅ Varied spacing creates rhythm
<section className="py-24 px-6">
  <h1 className="text-4xl font-bold mb-6">Title</h1>
  <div className="space-y-8 max-w-2xl">
    <p className="text-lg leading-relaxed">Important content</p>
    <p className="text-base text-gray-600">Secondary content</p>
  </div>
  <button className="mt-12">Action</button>
</section>
```

**Spacing Scale Best Practices**:
- Small gaps: 1, 2, 3 (4px-12px) - within components
- Medium gaps: 4, 6, 8 (16px-32px) - between elements
- Large gaps: 12, 16, 24 (48px-96px) - between sections
- Extra large: 32, 40, 48 (128px-192px) - major sections

---

### 5. Stock Gradient Backgrounds

**Problem**: Using obvious gradient backgrounds.

```jsx
// ❌ AI Pattern
<div className="bg-gradient-to-r from-purple-400 via-pink-500 to-red-500">
  <h1 className="text-white">Welcome</h1>
</div>
```

**Why It Looks AI-Generated**:
- Overly saturated colors
- Rainbow gradients rarely work
- Feels like a 2010s design
- Often reduces readability

**Professional Alternatives**:
```jsx
// ✅ Subtle gradient
<div className="bg-gradient-to-br from-gray-50 to-gray-100">
  <h1 className="text-gray-900">Welcome</h1>
</div>

// ✅ Monochromatic gradient
<div className="bg-gradient-to-b from-blue-600 to-blue-700">
  <h1 className="text-white">Welcome</h1>
</div>

// ✅ Pattern or texture instead
<div className="bg-slate-900 bg-[radial-gradient(circle_at_1px_1px,_rgb(148_163_184/0.15)_1px,_transparent_0)] bg-[size:40px_40px]">
  <h1 className="text-white">Welcome</h1>
</div>
```

---

### 6. Center-Aligned Everything

**Problem**: Centering all content without purpose.

```jsx
// ❌ AI Pattern
<div className="text-center">
  <h1>Welcome</h1>
  <p>This is some content that is centered for no particular reason.</p>
  <button>Action</button>
</div>
```

**Why It Looks AI-Generated**:
- Harder to read (especially long text)
- Lacks visual flow
- Feels amateurish for body content

**Professional Approach**:
```jsx
// ✅ Left-aligned with intentional centering
<div className="max-w-4xl mx-auto">
  <h1 className="text-center text-4xl font-bold mb-6">Welcome</h1>
  <p className="text-left text-lg leading-relaxed mb-8">
    This is content that flows naturally from left to right, 
    making it easier to read and more professional looking.
  </p>
  <div className="flex justify-start">
    <button>Action</button>
  </div>
</div>
```

**When to Center**:
- Headlines and hero sections
- Short CTAs (2-3 words)
- Single buttons in hero sections
- Pricing cards
- Testimonials

**When to Left-Align**:
- Body text (always)
- Form labels
- Lists
- Navigation items
- Most content

---

### 7. Generic Loading Spinners

**Problem**: Using basic spinning circle everywhere.

```jsx
// ❌ AI Pattern
{isLoading && (
  <div className="flex justify-center">
    <div className="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-500" />
  </div>
)}
```

**Why It Looks AI-Generated**:
- Generic and unpolished
- Doesn't match brand
- Provides no context
- Jarring layout shift

**Professional Alternatives**:
```jsx
// ✅ Skeleton screens
{isLoading ? (
  <div className="space-y-4 animate-pulse">
    <div className="h-4 bg-gray-200 rounded w-3/4" />
    <div className="h-4 bg-gray-200 rounded w-full" />
    <div className="h-4 bg-gray-200 rounded w-5/6" />
  </div>
) : (
  <Content />
)}

// ✅ Custom branded loader
{isLoading && (
  <div className="flex items-center gap-2">
    <div className="w-2 h-2 bg-blue-600 rounded-full animate-bounce [animation-delay:-0.3s]" />
    <div className="w-2 h-2 bg-blue-600 rounded-full animate-bounce [animation-delay:-0.15s]" />
    <div className="w-2 h-2 bg-blue-600 rounded-full animate-bounce" />
  </div>
)}
```

---

### 8. Missing Hover and Focus States

**Problem**: No visual feedback on interactive elements.

```jsx
// ❌ AI Pattern - No states
<button className="bg-blue-500 text-white px-4 py-2">
  Click me
</button>

<a href="/page" className="text-blue-500">
  Link
</a>
```

**Why It Looks AI-Generated**:
- No feedback when hovering
- No indication it's interactive
- Poor accessibility (no focus indicators)

**Professional States**:
```jsx
// ✅ Complete button states
<button className="
  bg-blue-600 text-white px-6 py-2.5 rounded-lg
  hover:bg-blue-700 hover:shadow-md
  active:scale-[0.98]
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
  disabled:opacity-50 disabled:cursor-not-allowed
  transition-all duration-200
">
  Click me
</button>

// ✅ Complete link states
<a href="/page" className="
  text-blue-600 font-medium
  hover:text-blue-700 hover:underline
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:rounded
  transition-colors
">
  Link
</a>
```

---

### 9. Generic Placeholder Content

**Problem**: Using obvious placeholders like "Lorem ipsum" or generic text.

```jsx
// ❌ AI Pattern
<div>
  <h1>Welcome to Our Website</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  <button>Click Here</button>
</div>
```

**Why It Looks AI-Generated**:
- "Welcome to Our Website" is too generic
- Lorem ipsum screams placeholder
- "Click Here" is poor UX

**Professional Content**:
```jsx
// ✅ Specific, purposeful content
<div>
  <h1>Ship better products, faster</h1>
  <p>
    Join 10,000+ teams using our platform to reduce development 
    time by 40% while maintaining quality.
  </p>
  <button>Start free trial</button>
</div>
```

---

### 10. Over-Reliance on Icons

**Problem**: Putting icons on everything without purpose.

```jsx
// ❌ AI Pattern - Icons everywhere
<button>
  <Icon name="check" /> Submit
</button>
<button>
  <Icon name="x" /> Cancel
</button>
<button>
  <Icon name="save" /> Save
</button>
```

**Why It Looks AI-Generated**:
- Icons don't add value
- Makes interface cluttered
- Slows down comprehension

**Professional Icon Usage**:
```jsx
// ✅ Icons only where they add value
<button>Submit</button>  // No icon needed
<button>Cancel</button>  // No icon needed

// Icons that add clarity:
<button>
  <SearchIcon /> Search
</button>

<button>
  Download Report <DownloadIcon />
</button>

// Icon-only (with accessibility):
<button aria-label="Close dialog">
  <XIcon />
</button>
```

**When to Use Icons**:
- Universal symbols (search, menu, close)
- Visual reinforcement (download, upload, external link)
- Space-constrained mobile UIs
- Navigation with labels

**When to Skip Icons**:
- Text is clear enough alone
- Icon meaning is ambiguous
- Would clutter the interface

---

## Layout Anti-Patterns

### 11. The "Everything in Cards" Pattern

**Problem**: Wrapping everything in card containers.

```jsx
// ❌ AI Pattern
<div className="grid grid-cols-3 gap-4">
  <Card><h3>Feature 1</h3></Card>
  <Card><h3>Feature 2</h3></Card>
  <Card><h3>Feature 3</h3></Card>
</div>
<div className="mt-4">
  <Card><p>Some content</p></Card>
</div>
```

**Professional Approach**:
```jsx
// ✅ Use cards purposefully
<div className="space-y-12">
  {/* No card needed for simple list */}
  <div className="grid grid-cols-3 gap-8">
    <Feature icon={Icon1} title="Feature 1" />
    <Feature icon={Icon2} title="Feature 2" />
    <Feature icon={Icon3} title="Feature 3" />
  </div>
  
  {/* Card appropriate for grouped content */}
  <Card>
    <CardHeader>
      <h3>Dashboard Stats</h3>
    </CardHeader>
    <CardContent>
      <Stats />
    </CardContent>
  </Card>
</div>
```

---

### 12. Ignoring Content Hierarchy

**Problem**: All content treated with equal visual weight.

```jsx
// ❌ AI Pattern
<div>
  <h1 className="text-2xl">Main Title</h1>
  <h2 className="text-xl">Subtitle</h2>
  <p className="text-lg">Body text</p>
  <span className="text-base">Caption</span>
</div>
```

**Professional Hierarchy**:
```jsx
// ✅ Clear visual hierarchy
<div className="space-y-6">
  <h1 className="text-5xl font-bold tracking-tight">
    Main Title
  </h1>
  <p className="text-xl text-gray-600">
    Subtitle
  </p>
  <p className="text-base text-gray-700 leading-relaxed max-w-2xl">
    Body text with proper line length and spacing
  </p>
  <span className="text-sm text-gray-500">
    Caption text
  </span>
</div>
```

---

## Typography Anti-Patterns

### 13. Poor Font Pairing

**Problem**: Using default system fonts or poor combinations.

```jsx
// ❌ AI Pattern
<div className="font-sans">
  <h1>Heading</h1>
  <p>Body text</p>
</div>
```

**Professional Font Pairing**:
```jsx
// ✅ Serif headline + Sans body
import { Playfair_Display, Inter } from 'next/font/google'

<div>
  <h1 className="font-serif text-5xl">Heading</h1>
  <p className="font-sans text-base">Body text</p>
</div>

// ✅ Display + Body
import { Space_Grotesk, Inter } from 'next/font/google'

<div>
  <h1 className="font-display text-5xl">Heading</h1>
  <p className="font-sans text-base">Body text</p>
</div>
```

---

### 14. Ignoring Line Length

**Problem**: Text spans full container width regardless of readability.

```jsx
// ❌ AI Pattern - Text too wide
<div className="w-full">
  <p>
    This is a very long line of text that spans the entire width 
    of the container making it very difficult to read especially 
    on large screens where it might be 150+ characters wide.
  </p>
</div>
```

**Professional Line Length**:
```jsx
// ✅ Optimal line length
<div className="max-w-2xl"> {/* ~65-75 characters */}
  <p className="text-lg leading-relaxed">
    This text is constrained to an optimal line length, 
    making it much more comfortable to read.
  </p>
</div>
```

**Line Length Guidelines**:
- Body text: 60-75 characters (max-w-2xl)
- Headlines: Can be wider (max-w-4xl)
- Captions: Can be narrower (max-w-md)

---

## Interaction Anti-Patterns

### 15. No Loading States

**Problem**: Button just becomes disabled with no indication.

```jsx
// ❌ AI Pattern
<button disabled={isLoading} onClick={handleSubmit}>
  Submit
</button>
```

**Professional Loading States**:
```jsx
// ✅ Clear loading indication
<button 
  disabled={isLoading}
  onClick={handleSubmit}
  className="relative"
>
  <span className={isLoading ? 'opacity-0' : ''}>
    Submit
  </span>
  {isLoading && (
    <span className="absolute inset-0 flex items-center justify-center">
      <LoadingSpinner />
    </span>
  )}
</button>
```

---

## Quick Checklist: Does My UI Look AI-Generated?

Check these telltale signs:

- [ ] All elements are perfectly centered or aligned
- [ ] Using bg-blue-500 or bg-green-500 for primary actions
- [ ] Every element has rounded-lg
- [ ] Spacing is uniform throughout (all p-4, gap-4, etc.)
- [ ] No hover or focus states
- [ ] Generic loading spinners
- [ ] Lorem ipsum or "Click here" text
- [ ] Cards everywhere
- [ ] No typography hierarchy
- [ ] Missing micro-interactions
- [ ] Stock gradients
- [ ] Icons on everything
- [ ] Text spans full width
- [ ] All same font size/weight

If you checked more than 3-4 items, your UI likely looks AI-generated.

---

## Conclusion

The key to avoiding AI-generated patterns is **intentionality**. Ask yourself:
- Why this color?
- Why this spacing?
- Why this layout?
- What purpose does this serve?

If you can't answer these questions, you're probably following AI-generated patterns. Professional design comes from purposeful decision-making.
