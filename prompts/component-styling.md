# Component Styling Improvement Prompt

## Context
You are refining component styling to move from generic AI-generated patterns to polished, professional designs that feel handcrafted.

## Button Improvements

### AI-Generated Button Issues
```jsx
// ❌ Generic AI-Generated Button
<button className="bg-blue-500 text-white px-4 py-2 rounded">
  Click me
</button>
```

### Professional Button Styling
```jsx
// ✅ Professional Button with Variants
<button className="
  inline-flex items-center justify-center
  px-6 py-2.5
  text-sm font-medium
  rounded-lg
  bg-blue-600 hover:bg-blue-700
  text-white
  transition-all duration-200
  shadow-sm hover:shadow-md
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
  active:scale-[0.98]
  disabled:opacity-50 disabled:cursor-not-allowed
">
  Click me
</button>

// Secondary variant
<button className="
  px-6 py-2.5
  text-sm font-medium
  rounded-lg
  bg-white hover:bg-gray-50
  text-gray-700
  border border-gray-300 hover:border-gray-400
  transition-all duration-200
  shadow-sm hover:shadow
  focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
">
  Cancel
</button>
```

## Card Components

### AI-Generated Card Issues
```jsx
// ❌ Generic Card
<div className="bg-white p-4 rounded shadow">
  <h3>Title</h3>
  <p>Content</p>
</div>
```

### Professional Card Styling
```jsx
// ✅ Professional Card with Hierarchy
<div className="
  bg-white
  rounded-xl
  shadow-sm hover:shadow-lg
  border border-gray-100
  transition-shadow duration-300
  overflow-hidden
  group
">
  <div className="p-6 space-y-4">
    <div className="flex items-start justify-between">
      <h3 className="text-lg font-semibold text-gray-900 leading-tight">
        Card Title
      </h3>
      <span className="px-2.5 py-1 text-xs font-medium rounded-full bg-blue-50 text-blue-700">
        New
      </span>
    </div>
    
    <p className="text-sm text-gray-600 leading-relaxed">
      Card content with proper typography and spacing
    </p>
    
    <div className="pt-4 border-t border-gray-100">
      <button className="
        text-sm font-medium text-blue-600 
        hover:text-blue-700 
        transition-colors
        group-hover:translate-x-1
        inline-flex items-center gap-2
      ">
        Learn more
        <svg className="w-4 h-4" /* arrow icon */ />
      </button>
    </div>
  </div>
</div>
```

## Form Inputs

### AI-Generated Input Issues
```jsx
// ❌ Generic Input
<input 
  type="text" 
  placeholder="Email"
  className="border p-2 rounded"
/>
```

### Professional Input Styling
```jsx
// ✅ Professional Input with States
<div className="space-y-2">
  <label className="block text-sm font-medium text-gray-700">
    Email address
  </label>
  <input 
    type="email"
    placeholder="you@example.com"
    className="
      w-full px-4 py-2.5
      text-sm text-gray-900
      placeholder:text-gray-400
      border border-gray-300
      rounded-lg
      bg-white
      transition-colors duration-200
      focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent
      hover:border-gray-400
      disabled:bg-gray-50 disabled:text-gray-500 disabled:cursor-not-allowed
    "
  />
  <p className="text-xs text-gray-500">
    We'll never share your email
  </p>
</div>

// ✅ Error State
<div className="space-y-2">
  <label className="block text-sm font-medium text-red-700">
    Email address
  </label>
  <input 
    type="email"
    className="
      w-full px-4 py-2.5
      text-sm text-gray-900
      border-2 border-red-300
      rounded-lg
      bg-red-50
      focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent
    "
  />
  <p className="text-xs text-red-600 flex items-center gap-1">
    <svg className="w-4 h-4" /* error icon */ />
    Please enter a valid email address
  </p>
</div>
```

## Navigation Components

### AI-Generated Nav Issues
```jsx
// ❌ Generic Navigation
<nav className="bg-white p-4 shadow">
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>
```

### Professional Navigation Styling
```jsx
// ✅ Professional Navigation
<nav className="bg-white border-b border-gray-200 sticky top-0 z-50 backdrop-blur-sm bg-white/90">
  <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div className="flex justify-between items-center h-16">
      {/* Logo */}
      <div className="flex items-center gap-3">
        <div className="w-8 h-8 bg-gradient-to-br from-blue-600 to-blue-700 rounded-lg" />
        <span className="text-xl font-semibold text-gray-900">Brand</span>
      </div>
      
      {/* Nav Links */}
      <div className="hidden md:flex items-center gap-1">
        <a href="/" className="
          px-4 py-2 rounded-lg
          text-sm font-medium text-blue-700 bg-blue-50
          transition-colors
        ">
          Home
        </a>
        <a href="/about" className="
          px-4 py-2 rounded-lg
          text-sm font-medium text-gray-600
          hover:text-gray-900 hover:bg-gray-50
          transition-colors
        ">
          About
        </a>
        <a href="/contact" className="
          px-4 py-2 rounded-lg
          text-sm font-medium text-gray-600
          hover:text-gray-900 hover:bg-gray-50
          transition-colors
        ">
          Contact
        </a>
      </div>
      
      {/* CTA */}
      <button className="
        px-4 py-2 rounded-lg
        text-sm font-medium text-white
        bg-blue-600 hover:bg-blue-700
        transition-colors
      ">
        Get Started
      </button>
    </div>
  </div>
</nav>
```

## Modal/Dialog Components

### AI-Generated Modal Issues
```jsx
// ❌ Generic Modal
<div className="fixed inset-0 bg-black bg-opacity-50">
  <div className="bg-white p-4 rounded">
    <h2>Modal Title</h2>
    <p>Content</p>
    <button>Close</button>
  </div>
</div>
```

### Professional Modal Styling
```jsx
// ✅ Professional Modal
<div className="
  fixed inset-0 z-50
  flex items-center justify-center
  p-4
  bg-gray-900/50 backdrop-blur-sm
  animate-in fade-in duration-200
">
  <div 
    className="
      w-full max-w-lg
      bg-white rounded-2xl
      shadow-2xl
      animate-in zoom-in-95 duration-200
      overflow-hidden
    "
    role="dialog"
    aria-modal="true"
  >
    {/* Header */}
    <div className="px-6 py-5 border-b border-gray-100">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-xl font-semibold text-gray-900">
            Modal Title
          </h2>
          <p className="mt-1 text-sm text-gray-500">
            Optional description text
          </p>
        </div>
        <button className="
          p-1 rounded-lg
          text-gray-400 hover:text-gray-600 hover:bg-gray-100
          transition-colors
        ">
          <svg className="w-5 h-5" /* close icon */ />
        </button>
      </div>
    </div>
    
    {/* Content */}
    <div className="px-6 py-5 space-y-4">
      <p className="text-sm text-gray-600 leading-relaxed">
        Modal content goes here with proper spacing and typography
      </p>
    </div>
    
    {/* Footer */}
    <div className="px-6 py-4 bg-gray-50 flex justify-end gap-3">
      <button className="
        px-4 py-2 rounded-lg
        text-sm font-medium text-gray-700
        bg-white hover:bg-gray-100
        border border-gray-300
        transition-colors
      ">
        Cancel
      </button>
      <button className="
        px-4 py-2 rounded-lg
        text-sm font-medium text-white
        bg-blue-600 hover:bg-blue-700
        transition-colors
      ">
        Confirm
      </button>
    </div>
  </div>
</div>
```

## Key Styling Principles

### 1. Consistent Spacing Scale
Use a systematic spacing scale (Tailwind's default is great):
- 0.5 = 2px, 1 = 4px, 2 = 8px, 3 = 12px, 4 = 16px
- 5 = 20px, 6 = 24px, 8 = 32px, 10 = 40px, 12 = 48px

### 2. Thoughtful Transitions
- Duration: 150-300ms for most interactions
- Use `transition-colors` for color changes
- Use `transition-all` sparingly (can be janky)
- Add `duration-200` or `duration-300` for smoothness

### 3. Focus States (Accessibility)
Always include visible focus states:
```jsx
focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
```

### 4. Hover States
Add subtle hover effects:
- Color changes: `hover:bg-blue-700`
- Shadows: `hover:shadow-lg`
- Scale: `hover:scale-105`
- Transforms: `hover:translate-x-1`

### 5. Active States
Show immediate feedback on click:
```jsx
active:scale-[0.98]
```

### 6. Disabled States
Make disabled states obvious:
```jsx
disabled:opacity-50 disabled:cursor-not-allowed
```

### 7. Group Interactions
Use group utilities for parent-child interactions:
```jsx
<div className="group">
  <span className="group-hover:translate-x-1">Arrow</span>
</div>
```

## Component Styling Checklist

- [ ] Use consistent spacing scale throughout
- [ ] Add smooth transitions (150-300ms)
- [ ] Include focus states for accessibility
- [ ] Add hover states for interactive elements
- [ ] Include active states for buttons
- [ ] Style disabled states appropriately
- [ ] Use shadows sparingly and purposefully
- [ ] Vary border radius (not everything needs rounded-lg)
- [ ] Use semantic color scales (gray-50 to gray-900)
- [ ] Add loading states for async actions
- [ ] Include error states for forms
- [ ] Use group interactions for related elements
- [ ] Add subtle animations where appropriate
- [ ] Ensure proper contrast ratios (WCAG AA)
- [ ] Test on different screen sizes
