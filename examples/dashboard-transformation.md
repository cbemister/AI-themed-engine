# Example: Dashboard Card Grid Transformation

This example shows how to transform a generic AI-generated dashboard card grid into a professional, engaging layout.

## Before: AI-Generated Dashboard

```jsx
// app/dashboard/page.jsx
export default function Dashboard() {
  return (
    <div className="p-4">
      <h1 className="text-2xl mb-4">Dashboard</h1>
      
      <div className="grid grid-cols-4 gap-4">
        <div className="bg-white p-4 rounded shadow">
          <h3 className="text-lg">Total Users</h3>
          <p className="text-2xl">1,234</p>
        </div>
        
        <div className="bg-white p-4 rounded shadow">
          <h3 className="text-lg">Revenue</h3>
          <p className="text-2xl">$45,678</p>
        </div>
        
        <div className="bg-white p-4 rounded shadow">
          <h3 className="text-lg">Active Now</h3>
          <p className="text-2xl">89</p>
        </div>
        
        <div className="bg-white p-4 rounded shadow">
          <h3 className="text-lg">Conversion</h3>
          <p className="text-2xl">2.4%</p>
        </div>
      </div>
    </div>
  )
}
```

### Issues Identified

1. ❌ **Uniform grid**: All cards exactly the same size
2. ❌ **Minimal padding**: `p-4` everywhere feels cramped
3. ❌ **Generic spacing**: `gap-4`, `mb-4` - no hierarchy
4. ❌ **Basic shadows**: Generic `shadow` class
5. ❌ **No hover states**: Cards feel static
6. ❌ **Poor typography**: Sizes too similar
7. ❌ **No color variation**: All white, boring
8. ❌ **Missing icons**: Numbers alone lack context
9. ❌ **No loading states**: No skeleton screens
10. ❌ **No data visualization**: Just raw numbers

---

## After: Professional Dashboard

```jsx
// app/dashboard/page.jsx
import { Suspense } from 'react'
import { 
  Users, 
  DollarSign, 
  Activity, 
  TrendingUp 
} from 'lucide-react'

export default function Dashboard() {
  return (
    <div className="min-h-screen bg-gray-50">
      <div className="max-w-7xl mx-auto px-6 py-12">
        {/* Header */}
        <div className="mb-12">
          <h1 className="text-4xl font-bold text-gray-900 mb-3">
            Dashboard
          </h1>
          <p className="text-lg text-gray-600">
            Welcome back! Here's what's happening today.
          </p>
        </div>
        
        {/* Stats Grid */}
        <Suspense fallback={<StatsGridSkeleton />}>
          <StatsGrid />
        </Suspense>
      </div>
    </div>
  )
}

async function StatsGrid() {
  // Fetch real data
  const stats = await getStats()
  
  return (
    <div className="grid grid-cols-12 gap-6">
      {/* Featured Card - Takes more space */}
      <div className="col-span-12 lg:col-span-7">
        <StatCard
          title="Total Revenue"
          value={stats.revenue}
          format="currency"
          change={+12.5}
          icon={DollarSign}
          trend={stats.revenueTrend}
          variant="featured"
        />
      </div>
      
      {/* Secondary Stats */}
      <div className="col-span-12 lg:col-span-5 grid grid-rows-2 gap-6">
        <StatCard
          title="Active Users"
          value={stats.activeUsers}
          format="number"
          change={+8.2}
          icon={Activity}
          variant="compact"
        />
        
        <StatCard
          title="Conversion Rate"
          value={stats.conversionRate}
          format="percentage"
          change={-2.4}
          icon={TrendingUp}
          variant="compact"
        />
      </div>
      
      {/* Bottom Row */}
      <div className="col-span-12 lg:col-span-6">
        <StatCard
          title="Total Users"
          value={stats.totalUsers}
          format="number"
          change={+15.3}
          icon={Users}
          subtitle="Across all regions"
        />
      </div>
      
      <div className="col-span-12 lg:col-span-6">
        <StatCard
          title="Average Session"
          value={stats.avgSession}
          format="duration"
          change={+5.1}
          icon={Activity}
          subtitle="User engagement time"
        />
      </div>
    </div>
  )
}

function StatCard({ 
  title, 
  value, 
  format, 
  change, 
  icon: Icon,
  trend,
  variant = 'default',
  subtitle 
}) {
  const isPositive = change >= 0
  const isFeatured = variant === 'featured'
  const isCompact = variant === 'compact'
  
  return (
    <div className={`
      group relative overflow-hidden
      bg-white rounded-2xl border border-gray-100
      transition-all duration-300
      hover:shadow-lg hover:border-gray-200
      ${isFeatured ? 'p-8' : 'p-6'}
      ${isCompact ? 'h-full' : ''}
    `}>
      {/* Background Gradient (subtle) */}
      <div className="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-blue-50 to-transparent rounded-full blur-3xl opacity-0 group-hover:opacity-100 transition-opacity" />
      
      {/* Content */}
      <div className="relative">
        {/* Header */}
        <div className="flex items-start justify-between mb-4">
          <div>
            <p className={`font-medium text-gray-600 ${isFeatured ? 'text-base' : 'text-sm'}`}>
              {title}
            </p>
            {subtitle && (
              <p className="text-xs text-gray-500 mt-1">{subtitle}</p>
            )}
          </div>
          
          {/* Icon */}
          <div className={`
            rounded-xl bg-blue-50 text-blue-600
            group-hover:bg-blue-100 transition-colors
            ${isFeatured ? 'p-3' : 'p-2.5'}
          `}>
            <Icon className={isFeatured ? 'w-6 h-6' : 'w-5 h-5'} />
          </div>
        </div>
        
        {/* Value */}
        <div className="mb-4">
          <p className={`font-bold text-gray-900 ${isFeatured ? 'text-5xl' : 'text-3xl'}`}>
            {formatValue(value, format)}
          </p>
        </div>
        
        {/* Change Indicator */}
        <div className="flex items-center gap-2">
          <span className={`
            inline-flex items-center gap-1 px-2 py-1 rounded-full text-xs font-medium
            ${isPositive 
              ? 'bg-green-50 text-green-700' 
              : 'bg-red-50 text-red-700'
            }
          `}>
            <svg 
              className={`w-3 h-3 ${!isPositive && 'rotate-180'}`}
              fill="currentColor" 
              viewBox="0 0 20 20"
            >
              <path d="M10 3l7 7h-4v7H7v-7H3l7-7z" />
            </svg>
            {Math.abs(change)}%
          </span>
          <span className="text-sm text-gray-600">
            vs last month
          </span>
        </div>
        
        {/* Trend Chart (for featured) */}
        {isFeatured && trend && (
          <div className="mt-6 h-16">
            <MiniChart data={trend} color={isPositive ? 'green' : 'red'} />
          </div>
        )}
      </div>
    </div>
  )
}

function MiniChart({ data, color }) {
  // Simplified sparkline chart
  const points = data.map((value, i) => {
    const x = (i / (data.length - 1)) * 100
    const y = 100 - (value / Math.max(...data)) * 100
    return `${x},${y}`
  }).join(' ')
  
  return (
    <svg className="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
      <polyline
        points={points}
        fill="none"
        stroke={color === 'green' ? '#10B981' : '#EF4444'}
        strokeWidth="2"
        className="opacity-50"
      />
    </svg>
  )
}

function formatValue(value, format) {
  switch (format) {
    case 'currency':
      return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 0,
      }).format(value)
    case 'percentage':
      return `${value}%`
    case 'duration':
      return `${value}m`
    default:
      return new Intl.NumberFormat('en-US').format(value)
  }
}

// Loading State
function StatsGridSkeleton() {
  return (
    <div className="grid grid-cols-12 gap-6 animate-pulse">
      <div className="col-span-7 h-64 bg-gray-200 rounded-2xl" />
      <div className="col-span-5 space-y-6">
        <div className="h-28 bg-gray-200 rounded-2xl" />
        <div className="h-28 bg-gray-200 rounded-2xl" />
      </div>
      <div className="col-span-6 h-48 bg-gray-200 rounded-2xl" />
      <div className="col-span-6 h-48 bg-gray-200 rounded-2xl" />
    </div>
  )
}
```

---

## What Improved

### 1. **Asymmetric Layout**
- ✅ Changed from uniform 4-column grid to 12-column system
- ✅ Featured card takes 7 columns (prominent)
- ✅ Secondary cards split remaining 5 columns
- ✅ Creates visual hierarchy and interest

### 2. **Better Spacing**
- ✅ Increased padding: `p-6` and `p-8` for featured
- ✅ Larger gaps: `gap-6` between cards
- ✅ Generous page padding: `px-6 py-12`
- ✅ Section spacing: `mb-12` for header

### 3. **Professional Typography**
- ✅ Larger header: `text-4xl` vs `text-2xl`
- ✅ Clear hierarchy: 5xl → 3xl → base → sm
- ✅ Font weights: Bold for numbers, medium for labels
- ✅ Color variation: gray-900 → gray-600 → gray-500

### 4. **Sophisticated Colors**
- ✅ Off-white background: `bg-gray-50` vs pure white page
- ✅ Subtle borders: `border-gray-100`
- ✅ Hover state: `hover:border-gray-200`
- ✅ Icon backgrounds: `bg-blue-50` with `text-blue-600`

### 5. **Complete Interactive States**
- ✅ Hover: Shadow increase + border color change
- ✅ Smooth transitions: `duration-300`
- ✅ Icon background color shift
- ✅ Gradient fade-in effect

### 6. **Visual Enhancements**
- ✅ Icons for context (not decoration)
- ✅ Change indicators with colors (green/red)
- ✅ Mini trend chart for featured card
- ✅ Subtle background gradient on hover

### 7. **Better Information Design**
- ✅ Subtitles for additional context
- ✅ Comparison metrics ("vs last month")
- ✅ Formatted values (currency, percentage, duration)
- ✅ Visual change indicators (arrows)

### 8. **Next.js Best Practices**
- ✅ Suspense for loading states
- ✅ Skeleton screens matching layout
- ✅ Async data fetching
- ✅ Proper component structure

### 9. **Professional Polish**
- ✅ Rounded corners: `rounded-2xl` (more modern)
- ✅ Shadow progression: none → hover:shadow-lg
- ✅ Border: `border-gray-100` for subtle depth
- ✅ Blur effect on hover gradient

### 10. **Accessibility**
- ✅ Semantic HTML structure
- ✅ Proper heading hierarchy
- ✅ Color not sole indicator (arrows + text)
- ✅ Good contrast ratios

---

## Key Differences Breakdown

| Aspect | Before | After |
|--------|--------|-------|
| **Layout** | Uniform 4-column | Asymmetric 12-column with featured card |
| **Padding** | p-4 (16px) | p-6 to p-8 (24px-32px) |
| **Typography** | text-2xl, text-lg | text-5xl, text-4xl, text-3xl hierarchy |
| **Colors** | All white, basic | Gray-50 background, blue-50 accents |
| **Shadows** | Generic shadow | shadow-lg on hover only |
| **Borders** | None | Subtle gray-100, changes on hover |
| **Icons** | None | Contextual with colored backgrounds |
| **States** | Static | Hover effects, transitions |
| **Data** | Raw numbers | Formatted + trend + comparison |
| **Loading** | None | Skeleton screens matching layout |

---

## Usage

```jsx
// In your Next.js app
// app/dashboard/page.jsx

import Dashboard from './Dashboard'

export const metadata = {
  title: 'Dashboard | Your App',
  description: 'View your dashboard metrics and analytics',
}

export default Dashboard
```

---

## Pro Tips

1. **Asymmetry Creates Interest**: Featured card at 58% width (7/12) feels more dynamic than 50%
2. **Vary Card Heights**: Not all cards need to be the same height
3. **Icons Add Context**: But use sparingly - only when they clarify meaning
4. **Show Trends**: Mini charts or arrows help users understand direction
5. **Format Numbers**: $45,678 is clearer than 45678
6. **Skeleton Screens**: Match your actual layout for smooth transitions
7. **Subtle Animations**: 300ms transitions feel smooth without being distracting
8. **Color Psychology**: Green = positive, Red = negative (but add icons too for accessibility)

---

## Learn More

- See [`docs/design-principles.md`](../docs/design-principles.md) for layout principles
- See [`prompts/component-styling.md`](../prompts/component-styling.md) for card patterns
- See [`docs/anti-patterns.md`](../docs/anti-patterns.md) for what to avoid

This dashboard went from generic AI-generated to professional by:
1. Breaking perfect symmetry
2. Creating visual hierarchy
3. Adding intentional spacing
4. Including meaningful micro-interactions
5. Providing context through icons and trends

The result: A dashboard that looks handcrafted, not generated.
