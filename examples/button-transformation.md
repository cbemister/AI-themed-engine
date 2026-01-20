# Example: Button Transformation

This example demonstrates how to transform an AI-generated button into a professional, polished component.

## Before: AI-Generated Button

```jsx
// components/Button.jsx
export function Button({ children, onClick }) {
  return (
    <button 
      onClick={onClick}
      className="bg-blue-500 text-white px-4 py-2 rounded"
    >
      {children}
    </button>
  )
}
```

### Issues Identified

1. ❌ **Generic color**: `bg-blue-500` is the default AI choice
2. ❌ **No hover state**: No visual feedback
3. ❌ **No focus state**: Poor accessibility
4. ❌ **No active state**: No press feedback
5. ❌ **No disabled state**: Can't show disabled
6. ❌ **No variants**: Only one style
7. ❌ **No loading state**: Can't show async actions
8. ❌ **Abrupt transitions**: No smooth animations
9. ❌ **Generic spacing**: Standard px-4 py-2
10. ❌ **Single border radius**: Only one option

---

## After: Professional Button

```jsx
// components/Button.jsx
import { forwardRef } from 'react'
import { cva, type VariantProps } from 'class-variance-authority'

const buttonVariants = cva(
  // Base styles
  'inline-flex items-center justify-center rounded-lg font-medium transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed',
  {
    variants: {
      variant: {
        primary: 
          'bg-blue-600 text-white hover:bg-blue-700 active:bg-blue-800 focus:ring-blue-500 shadow-sm hover:shadow-md',
        secondary:
          'bg-white text-gray-700 border border-gray-300 hover:bg-gray-50 hover:border-gray-400 active:bg-gray-100 focus:ring-blue-500 shadow-sm',
        ghost:
          'bg-transparent text-blue-600 hover:bg-blue-50 active:bg-blue-100 focus:ring-blue-500',
        danger:
          'bg-red-600 text-white hover:bg-red-700 active:bg-red-800 focus:ring-red-500 shadow-sm hover:shadow-md',
      },
      size: {
        sm: 'px-3 py-1.5 text-sm',
        md: 'px-6 py-2.5 text-sm',
        lg: 'px-8 py-3 text-base',
      },
    },
    defaultVariants: {
      variant: 'primary',
      size: 'md',
    },
  }
)

export interface ButtonProps
  extends React.ButtonHTMLAttributes<HTMLButtonElement>,
    VariantProps<typeof buttonVariants> {
  isLoading?: boolean
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant, size, isLoading, children, disabled, ...props }, ref) => {
    return (
      <button
        ref={ref}
        className={buttonVariants({ variant, size, className })}
        disabled={disabled || isLoading}
        {...props}
      >
        {isLoading ? (
          <>
            <svg
              className="animate-spin -ml-1 mr-2 h-4 w-4"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <circle
                className="opacity-25"
                cx="12"
                cy="12"
                r="10"
                stroke="currentColor"
                strokeWidth="4"
              />
              <path
                className="opacity-75"
                fill="currentColor"
                d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
              />
            </svg>
            Loading...
          </>
        ) : (
          children
        )}
      </button>
    )
  }
)

Button.displayName = 'Button'
```

---

## Usage Examples

```jsx
import { Button } from '@/components/Button'

export function Examples() {
  return (
    <div className="space-y-8 p-8">
      {/* Primary Buttons */}
      <div className="space-y-4">
        <h3 className="text-lg font-semibold">Primary</h3>
        <div className="flex gap-4 items-center">
          <Button size="sm">Small</Button>
          <Button size="md">Medium</Button>
          <Button size="lg">Large</Button>
          <Button isLoading>Loading</Button>
          <Button disabled>Disabled</Button>
        </div>
      </div>

      {/* Secondary Buttons */}
      <div className="space-y-4">
        <h3 className="text-lg font-semibold">Secondary</h3>
        <div className="flex gap-4 items-center">
          <Button variant="secondary" size="sm">Small</Button>
          <Button variant="secondary" size="md">Medium</Button>
          <Button variant="secondary" size="lg">Large</Button>
          <Button variant="secondary" isLoading>Loading</Button>
          <Button variant="secondary" disabled>Disabled</Button>
        </div>
      </div>

      {/* Ghost Buttons */}
      <div className="space-y-4">
        <h3 className="text-lg font-semibold">Ghost</h3>
        <div className="flex gap-4 items-center">
          <Button variant="ghost" size="sm">Small</Button>
          <Button variant="ghost" size="md">Medium</Button>
          <Button variant="ghost" size="lg">Large</Button>
          <Button variant="ghost" disabled>Disabled</Button>
        </div>
      </div>

      {/* Danger Buttons */}
      <div className="space-y-4">
        <h3 className="text-lg font-semibold">Danger</h3>
        <div className="flex gap-4 items-center">
          <Button variant="danger" size="sm">Delete</Button>
          <Button variant="danger" size="md">Delete</Button>
          <Button variant="danger" size="lg">Delete</Button>
          <Button variant="danger" disabled>Delete</Button>
        </div>
      </div>
    </div>
  )
}
```

---

## What Improved

### 1. **Color Sophistication**
- ✅ Changed from `bg-blue-500` to `bg-blue-600` (deeper, more professional)
- ✅ Added proper hover state: `hover:bg-blue-700`
- ✅ Added active state: `active:bg-blue-800`

### 2. **Complete Interactive States**
- ✅ Hover: Color change + shadow increase
- ✅ Focus: Ring indicator for keyboard users
- ✅ Active: Pressed state feedback
- ✅ Disabled: Reduced opacity + cursor change
- ✅ Loading: Spinner with smooth animation

### 3. **Multiple Variants**
- ✅ Primary: Main actions
- ✅ Secondary: Alternative actions
- ✅ Ghost: Tertiary actions
- ✅ Danger: Destructive actions

### 4. **Size Variants**
- ✅ Small: Compact spaces
- ✅ Medium: Default
- ✅ Large: Hero sections, emphasis

### 5. **Smooth Transitions**
- ✅ `transition-all duration-200` for smooth state changes
- ✅ Shadow transitions for depth changes
- ✅ Color transitions feel responsive

### 6. **Better Spacing**
- ✅ Increased from `px-4 py-2` to `px-6 py-2.5` for better proportions
- ✅ Size-appropriate padding for each variant

### 7. **Professional Shadows**
- ✅ `shadow-sm` at rest
- ✅ `shadow-md` on hover
- ✅ Creates subtle depth

### 8. **Accessibility**
- ✅ Focus ring indicator
- ✅ Ring offset for visibility
- ✅ Proper disabled state
- ✅ Loading state announced to screen readers

### 9. **Type Safety**
- ✅ TypeScript support
- ✅ Proper prop types
- ✅ Autocomplete for variants

### 10. **Maintainability**
- ✅ Uses class-variance-authority for variant management
- ✅ Easy to extend with new variants
- ✅ Consistent API

---

## Installation

If you want to use this button in your project:

```bash
# Install dependencies
npm install class-variance-authority clsx tailwind-merge

# Or if using the simpler version, just copy the component
```

---

## Simplified Version (No Dependencies)

If you don't want to use class-variance-authority:

```jsx
// components/Button.jsx
export function Button({ 
  children, 
  onClick,
  variant = 'primary',
  size = 'md',
  isLoading = false,
  disabled = false,
  className = '',
  ...props 
}) {
  const baseStyles = 'inline-flex items-center justify-center rounded-lg font-medium transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed'
  
  const variants = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700 active:bg-blue-800 focus:ring-blue-500 shadow-sm hover:shadow-md',
    secondary: 'bg-white text-gray-700 border border-gray-300 hover:bg-gray-50 hover:border-gray-400 active:bg-gray-100 focus:ring-blue-500 shadow-sm',
    ghost: 'bg-transparent text-blue-600 hover:bg-blue-50 active:bg-blue-100 focus:ring-blue-500',
    danger: 'bg-red-600 text-white hover:bg-red-700 active:bg-red-800 focus:ring-red-500 shadow-sm hover:shadow-md',
  }
  
  const sizes = {
    sm: 'px-3 py-1.5 text-sm',
    md: 'px-6 py-2.5 text-sm',
    lg: 'px-8 py-3 text-base',
  }
  
  return (
    <button
      onClick={onClick}
      disabled={disabled || isLoading}
      className={`${baseStyles} ${variants[variant]} ${sizes[size]} ${className}`}
      {...props}
    >
      {isLoading ? (
        <>
          <svg
            className="animate-spin -ml-1 mr-2 h-4 w-4"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
          >
            <circle
              className="opacity-25"
              cx="12"
              cy="12"
              r="10"
              stroke="currentColor"
              strokeWidth="4"
            />
            <path
              className="opacity-75"
              fill="currentColor"
              d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
            />
          </svg>
          Loading...
        </>
      ) : (
        children
      )}
    </button>
  )
}
```

---

## Key Takeaways

1. **Move from blue-500 to blue-600+**: Deeper tones feel more professional
2. **Always include hover/focus/active states**: Essential for UX
3. **Add loading states**: Users need feedback for async actions
4. **Use smooth transitions**: 200-300ms feels responsive
5. **Create variants**: Different contexts need different styles
6. **Add shadows**: Subtle depth improves visual hierarchy
7. **Think about accessibility**: Focus states, disabled states, screen readers
8. **Proper spacing**: Generous padding feels more polished
9. **Type safety**: TypeScript helps prevent errors
10. **Consistent API**: Easy to use and maintain

This button went from looking obviously AI-generated to professional and production-ready by addressing each of these areas systematically.
