# Accessibility Improvement Prompt

## Context
You are improving the accessibility of AI-generated UI designs to ensure they are usable by everyone, including people with disabilities. AI-generated UIs often miss critical accessibility features.

## Common AI-Generated Accessibility Issues

### 1. Missing ARIA Labels
**Problem**: AI often creates buttons and links without proper labels

```jsx
// ❌ AI-Generated - No accessible name
<button className="p-2">
  <svg>...</svg>
</button>

// ✅ Improved - Proper accessible name
<button 
  className="p-2"
  aria-label="Close dialog"
>
  <svg aria-hidden="true">...</svg>
</button>
```

### 2. Poor Color Contrast
**Problem**: AI uses colors that don't meet WCAG contrast requirements

```jsx
// ❌ AI-Generated - Insufficient contrast
<p className="text-gray-400 bg-white">
  Important information
</p>

// ✅ Improved - WCAG AA compliant (4.5:1 minimum)
<p className="text-gray-700 bg-white">
  Important information
</p>
```

### 3. Missing Focus Indicators
**Problem**: AI removes or doesn't include visible focus states

```jsx
// ❌ AI-Generated - No focus indicator
<button className="outline-none">
  Submit
</button>

// ✅ Improved - Clear focus indicator
<button className="
  focus:outline-none 
  focus:ring-2 
  focus:ring-blue-500 
  focus:ring-offset-2
">
  Submit
</button>
```

### 4. Non-Semantic HTML
**Problem**: AI uses divs and spans instead of semantic elements

```jsx
// ❌ AI-Generated - Divs for everything
<div onClick={handleClick}>
  <div>Heading</div>
  <div>Some content</div>
</div>

// ✅ Improved - Semantic HTML
<article>
  <h2>Heading</h2>
  <p>Some content</p>
  <button onClick={handleClick}>Action</button>
</article>
```

### 5. Missing Alt Text
**Problem**: Images without descriptive alt text

```jsx
// ❌ AI-Generated
<img src="/user.jpg" />

// ✅ Improved - Descriptive alt text
<Image 
  src="/user.jpg" 
  alt="Profile photo of Jane Smith, smiling in front of office building"
  width={200}
  height={200}
/>

// ✅ Decorative images
<img src="/decoration.svg" alt="" role="presentation" />
```

### 6. Inaccessible Forms
**Problem**: Forms without proper labels and error handling

```jsx
// ❌ AI-Generated - Placeholder as label
<input type="email" placeholder="Email" />

// ✅ Improved - Proper labels and error states
<div>
  <label htmlFor="email" className="block text-sm font-medium mb-2">
    Email address
  </label>
  <input 
    type="email"
    id="email"
    name="email"
    aria-describedby="email-error"
    aria-invalid={hasError}
    className="..."
  />
  {hasError && (
    <p id="email-error" className="mt-2 text-sm text-red-600" role="alert">
      Please enter a valid email address
    </p>
  )}
</div>
```

## Essential Accessibility Features

### 1. Keyboard Navigation
All interactive elements must be keyboard accessible:

```jsx
// ✅ Keyboard accessible custom dropdown
<div className="relative">
  <button
    onClick={toggle}
    onKeyDown={(e) => {
      if (e.key === 'ArrowDown') {
        e.preventDefault()
        setOpen(true)
        // Focus first item
      }
    }}
    aria-haspopup="listbox"
    aria-expanded={isOpen}
    aria-labelledby="dropdown-label"
  >
    Select option
  </button>
  
  {isOpen && (
    <ul 
      role="listbox"
      onKeyDown={handleListKeyboard}
    >
      <li 
        role="option" 
        tabIndex={0}
        aria-selected={isSelected}
      >
        Option 1
      </li>
    </ul>
  )}
</div>
```

### 2. Screen Reader Support
Provide context for screen reader users:

```jsx
// ✅ Screen reader friendly loading state
<button disabled={isLoading}>
  {isLoading ? (
    <>
      <span className="sr-only">Loading, please wait...</span>
      <svg className="animate-spin" aria-hidden="true">...</svg>
    </>
  ) : (
    'Submit'
  )}
</button>

// ✅ Skip navigation link
<a 
  href="#main-content" 
  className="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 focus:z-50"
>
  Skip to main content
</a>
```

### 3. Live Regions
Announce dynamic changes to screen readers:

```jsx
// ✅ Live region for notifications
<div 
  role="status" 
  aria-live="polite" 
  aria-atomic="true"
  className="sr-only"
>
  {notification && notification.message}
</div>

// ✅ Alert for errors
<div 
  role="alert" 
  aria-live="assertive"
>
  {error && error.message}
</div>
```

### 4. Modal Dialogs
Properly trap focus and manage focus:

```jsx
'use client'
import { useEffect, useRef } from 'react'
import { createPortal } from 'react-dom'

export function Modal({ isOpen, onClose, children }) {
  const modalRef = useRef(null)
  const previousActiveElement = useRef(null)

  useEffect(() => {
    if (isOpen) {
      // Store current focus
      previousActiveElement.current = document.activeElement
      
      // Focus modal
      modalRef.current?.focus()
      
      // Trap focus
      const focusableElements = modalRef.current?.querySelectorAll(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
      )
      
      const handleKeyDown = (e) => {
        if (e.key === 'Escape') {
          onClose()
        }
        
        if (e.key === 'Tab') {
          const firstElement = focusableElements[0]
          const lastElement = focusableElements[focusableElements.length - 1]
          
          if (e.shiftKey && document.activeElement === firstElement) {
            e.preventDefault()
            lastElement.focus()
          } else if (!e.shiftKey && document.activeElement === lastElement) {
            e.preventDefault()
            firstElement.focus()
          }
        }
      }
      
      document.addEventListener('keydown', handleKeyDown)
      return () => document.removeEventListener('keydown', handleKeyDown)
    } else {
      // Restore focus
      previousActiveElement.current?.focus()
    }
  }, [isOpen, onClose])

  if (!isOpen) return null

  return createPortal(
    <div 
      className="fixed inset-0 z-50 bg-black/50"
      onClick={onClose}
    >
      <div
        ref={modalRef}
        role="dialog"
        aria-modal="true"
        aria-labelledby="modal-title"
        tabIndex={-1}
        className="..."
        onClick={(e) => e.stopPropagation()}
      >
        {children}
      </div>
    </div>,
    document.body
  )
}
```

### 5. Responsive and Mobile-Friendly
Ensure touch targets are large enough:

```jsx
// ✅ Minimum 44x44px touch targets
<button className="min-h-[44px] min-w-[44px] p-3">
  Icon
</button>

// ✅ Mobile-friendly navigation
<nav className="md:flex">
  <button 
    className="md:hidden p-3 min-h-[44px] min-w-[44px]"
    aria-label="Open menu"
    aria-expanded={isOpen}
  >
    <MenuIcon />
  </button>
  
  <div className={`
    ${isOpen ? 'block' : 'hidden'} 
    md:block
  `}>
    {/* Menu items */}
  </div>
</nav>
```

## WCAG 2.1 Level AA Checklist

### Perceivable
- [ ] All images have alt text (or alt="" for decorative)
- [ ] Text has minimum 4.5:1 contrast ratio (3:1 for large text)
- [ ] Color is not the only means of conveying information
- [ ] Text can be resized up to 200% without loss of functionality
- [ ] Content is structured with proper headings (h1-h6)

### Operable
- [ ] All functionality available via keyboard
- [ ] No keyboard traps
- [ ] Visible focus indicators on all interactive elements
- [ ] Sufficient time for users to read and interact
- [ ] Page has descriptive title
- [ ] Link purpose is clear from link text or context
- [ ] Multiple ways to navigate (menu, search, sitemap)
- [ ] Skip links available

### Understandable
- [ ] Language of page is identified (lang attribute)
- [ ] Forms have labels and instructions
- [ ] Error messages are clear and helpful
- [ ] Error prevention for important actions (confirmation)
- [ ] Consistent navigation across pages
- [ ] Consistent identification of components

### Robust
- [ ] Valid HTML (proper nesting, unique IDs)
- [ ] ARIA used correctly
- [ ] Status messages announced to screen readers
- [ ] Works with assistive technologies

## Testing Tools & Techniques

### Automated Testing
```bash
# Install axe-core for accessibility testing
npm install -D @axe-core/react

# Use in your Next.js app
# pages/_app.js (development only)
if (process.env.NODE_ENV !== 'production') {
  import('@axe-core/react').then((axe) => {
    axe.default(React, ReactDOM, 1000)
  })
}
```

### Manual Testing
1. **Keyboard Only**: Navigate entire site using only keyboard (Tab, Enter, Arrow keys, Esc)
2. **Screen Reader**: Test with NVDA (Windows), JAWS (Windows), or VoiceOver (Mac)
3. **Color Contrast**: Use browser DevTools or WebAIM contrast checker
4. **Zoom to 200%**: Ensure layout still works and text is readable
5. **Mobile**: Test on actual mobile devices with screen readers

### Browser Extensions
- axe DevTools
- WAVE (Web Accessibility Evaluation Tool)
- Lighthouse (built into Chrome DevTools)
- Color Contrast Analyzer

## Quick Wins for Better Accessibility

1. **Use semantic HTML**: `<button>` not `<div onClick>`
2. **Add focus styles**: Never use `outline: none` without replacement
3. **Label everything**: Every input needs a `<label>`
4. **Alt text**: Every `<img>` needs alt attribute
5. **Heading structure**: Use proper hierarchy (h1 → h2 → h3)
6. **ARIA sparingly**: Native HTML is usually better
7. **Test with keyboard**: If you can't use it with keyboard, it's broken
8. **Color contrast**: Use tools to check, don't guess

## Accessibility Improvement Process

1. **Audit**: Run automated tools (Lighthouse, axe)
2. **Manual Test**: Use keyboard and screen reader
3. **Fix Issues**: Address problems in priority order
4. **Retest**: Verify fixes work
5. **Document**: Note any limitations or known issues

Remember: Accessibility is not optional. It's a legal requirement in many jurisdictions and, more importantly, it's the right thing to do.
