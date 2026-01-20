# Claude Skills for AI Theme Engine

## Overview

This document defines reusable skills that can be used with Claude to systematically improve AI-generated UI designs. These skills can be combined and chained for comprehensive UI improvements.

## Skill 1: UI Analysis and Pattern Detection

**Purpose**: Analyze UI code to identify AI-generated patterns and areas for improvement.

**Inputs**:
- Component code (JSX/TSX)
- Framework context (Next.js, React, etc.)

**Process**:
1. Scan for telltale AI patterns:
   - Uniform spacing (repeated p-4, gap-4, etc.)
   - Generic colors (bg-blue-500, bg-green-500)
   - Perfect symmetry in layouts
   - Missing interactive states
   - Uniform border radius (rounded-lg everywhere)
2. Evaluate typography hierarchy
3. Check color sophistication
4. Assess spacing intentionality
5. Review accessibility features

**Outputs**:
- List of identified AI patterns
- Severity rating for each issue
- Suggested improvement priority
- Specific line numbers/code sections

**Example Usage**:
```
Using the UI Analysis skill, analyze this component:
[paste component code]

Identify AI-generated patterns and prioritize improvements.
```

---

## Skill 2: Color Palette Refinement

**Purpose**: Transform generic color schemes into sophisticated, professional palettes.

**Inputs**:
- Current color values (hex, rgb, or Tailwind classes)
- Brand personality (if known)
- Design context (SaaS, e-commerce, blog, etc.)

**Process**:
1. Identify oversaturated or generic colors
2. Generate refined alternatives:
   - Deeper tones for primary actions
   - Muted backgrounds
   - Sophisticated accent colors
3. Ensure WCAG AA contrast compliance
4. Create complete color scale (50-900)
5. Define semantic colors (success, warning, error, info)

**Outputs**:
- Refined color palette with hex values
- Tailwind configuration (if applicable)
- Before/after comparison
- Contrast ratio verification

**Example Usage**:
```
Using the Color Palette Refinement skill, improve these colors:
- Primary: #3B82F6 (blue-500)
- Secondary: #10B981 (green-500)
- Background: #FFFFFF

Context: SaaS dashboard, professional and trustworthy
```

---

## Skill 3: Typography System Design

**Purpose**: Create a cohesive typography system with proper hierarchy and readability.

**Inputs**:
- Current font choices and sizes
- Brand personality
- Content types (marketing, documentation, application, etc.)

**Process**:
1. Recommend font pairings (serif + sans, display + body, etc.)
2. Define type scale (8-10 sizes)
3. Establish weight hierarchy (400, 600, 700)
4. Set line heights for each context
5. Define letter spacing rules
6. Create responsive sizing strategy

**Outputs**:
- Complete typography system
- Font loading code (Next.js font optimization)
- Tailwind configuration
- Usage guidelines for each size/weight

**Example Usage**:
```
Using the Typography System Design skill, create a typography system for:
- A modern SaaS application
- Clean, professional aesthetic
- Needs to work for marketing and application pages
```

---

## Skill 4: Spacing System Optimization

**Purpose**: Transform uniform spacing into intentional, hierarchical spacing that creates visual rhythm.

**Inputs**:
- Current spacing values
- Layout structure
- Content hierarchy

**Process**:
1. Identify uniform spacing patterns
2. Define spacing scale (4px base unit)
3. Apply spacing based on hierarchy:
   - Tight spacing: related elements
   - Medium spacing: sections
   - Large spacing: major divisions
4. Create rhythm through varied spacing
5. Ensure responsive spacing (mobile to desktop)

**Outputs**:
- Updated spacing values
- Before/after code comparison
- Spacing scale reference
- Usage guidelines

**Example Usage**:
```
Using the Spacing System Optimization skill, improve spacing in this component:
[paste component with uniform spacing]

Create visual hierarchy and rhythm.
```

---

## Skill 5: Component State Enhancement

**Purpose**: Add complete interactive states (hover, focus, active, disabled, loading) to components.

**Inputs**:
- Component code
- Component type (button, link, input, card, etc.)
- Brand colors

**Process**:
1. Identify missing states
2. Add hover states with subtle transitions
3. Implement focus indicators for accessibility
4. Create active/pressed states
5. Design disabled states
6. Add loading states where applicable
7. Ensure smooth transitions (200-300ms)

**Outputs**:
- Updated component with all states
- Transition specifications
- Accessibility considerations

**Example Usage**:
```
Using the Component State Enhancement skill, add complete states to:
[paste button/input/component code]
```

---

## Skill 6: Layout Asymmetry Introduction

**Purpose**: Break perfect symmetry and create more engaging, professional layouts.

**Inputs**:
- Current layout code
- Content priorities
- Design goals

**Process**:
1. Analyze current symmetry
2. Identify opportunities for asymmetry
3. Apply 60/40 or 70/30 splits instead of 50/50
4. Vary content block sizes
5. Create focal points
6. Maintain visual balance (not symmetry)

**Outputs**:
- Refined layout code
- Visual hierarchy improvements
- Explanation of changes

**Example Usage**:
```
Using the Layout Asymmetry Introduction skill, transform this symmetric layout:
[paste grid/layout code]
```

---

## Skill 7: Accessibility Audit and Fix

**Purpose**: Identify and fix accessibility issues to meet WCAG 2.1 Level AA standards.

**Inputs**:
- Component or page code
- Target WCAG level (AA or AAA)

**Process**:
1. Check semantic HTML usage
2. Verify color contrast ratios
3. Ensure keyboard navigation works
4. Check focus indicators
5. Verify ARIA usage (correct/necessary)
6. Test form labels and error messages
7. Check alt text on images
8. Verify heading hierarchy

**Outputs**:
- List of accessibility issues
- Fixed code
- Testing recommendations
- WCAG compliance checklist

**Example Usage**:
```
Using the Accessibility Audit and Fix skill, review this component:
[paste component code]

Target: WCAG 2.1 Level AA compliance
```

---

## Skill 8: Next.js Optimization

**Purpose**: Apply Next.js-specific optimizations for better performance and UX.

**Inputs**:
- Next.js component code
- Next.js version (13+ App Router or Pages Router)
- Performance goals

**Process**:
1. Convert to Server Components where possible
2. Add loading.js for loading states
3. Implement error.js for error handling
4. Optimize images with next/image
5. Implement font optimization with next/font
6. Add proper metadata for SEO
7. Use Suspense for streaming
8. Implement parallel data fetching

**Outputs**:
- Optimized Next.js code
- Performance improvements list
- SEO enhancements
- File structure recommendations

**Example Usage**:
```
Using the Next.js Optimization skill, optimize this Next.js 13+ component:
[paste component code]

Focus on performance and SEO.
```

---

## Skill 9: Micro-Interaction Design

**Purpose**: Add subtle animations and transitions that make interfaces feel responsive and alive.

**Inputs**:
- Component code
- Interaction points (buttons, links, cards, etc.)
- Animation style preference (subtle, playful, minimal)

**Process**:
1. Identify interaction opportunities
2. Design hover effects (scale, shadow, color)
3. Add press/active states
4. Create entrance/exit animations
5. Implement loading animations
6. Add smooth transitions (ease-out/ease-in)
7. Ensure 60fps performance

**Outputs**:
- Enhanced component with micro-interactions
- Animation specifications
- Performance considerations

**Example Usage**:
```
Using the Micro-Interaction Design skill, add subtle interactions to:
[paste component code]

Style: Subtle and professional
```

---

## Skill 10: Component Polish Pass

**Purpose**: Final polish pass to elevate a component from good to excellent.

**Inputs**:
- Component code
- Design system context

**Process**:
1. Review and refine all previous improvements
2. Check consistency with design system
3. Add subtle details (shadows, borders, gradients)
4. Perfect spacing and alignment
5. Ensure all states are covered
6. Add skeleton loading states
7. Implement error states
8. Final accessibility check

**Outputs**:
- Polished component code
- Polish checklist
- Final recommendations

**Example Usage**:
```
Using the Component Polish Pass skill, perform final polish on:
[paste component code]

Ensure professional, production-ready quality.
```

---

## Skill Chaining Workflows

### Workflow 1: Complete Component Transformation

1. **UI Analysis** → Identify issues
2. **Color Palette Refinement** → Fix colors
3. **Typography System Design** → Improve text
4. **Spacing System Optimization** → Fix spacing
5. **Component State Enhancement** → Add states
6. **Accessibility Audit** → Ensure accessibility
7. **Micro-Interaction Design** → Add polish
8. **Component Polish Pass** → Final review

### Workflow 2: Layout Improvement

1. **UI Analysis** → Identify layout issues
2. **Layout Asymmetry Introduction** → Break symmetry
3. **Spacing System Optimization** → Create rhythm
4. **Component Polish Pass** → Final polish

### Workflow 3: Next.js Page Optimization

1. **UI Analysis** → Identify issues
2. **Next.js Optimization** → Apply framework features
3. **Accessibility Audit** → Ensure accessibility
4. **Component Polish Pass** → Final review

---

## Using Multiple Skills

You can invoke multiple skills in a single request:

```
Please improve this component using:
1. UI Analysis skill - identify issues
2. Color Palette Refinement skill - improve colors
3. Component State Enhancement skill - add missing states
4. Accessibility Audit skill - ensure WCAG AA compliance

[paste component code]
```

---

## Skill Parameters

Each skill can be customized with parameters:

**Intensity Levels**:
- `minimal`: Small, safe improvements
- `moderate`: Balanced improvements (default)
- `aggressive`: Significant transformation

**Style Preferences**:
- `minimal`: Clean, lots of whitespace
- `modern`: Current trends, subtle effects
- `playful`: More personality and animation
- `professional`: Conservative, trustworthy

**Framework**:
- `nextjs-13`: Next.js 13+ App Router
- `nextjs-pages`: Next.js Pages Router
- `react`: Plain React
- `remix`: Remix framework

---

## Example: Full Component Improvement

```
I have a login form component that looks AI-generated. 
Please use these skills in sequence:

1. UI Analysis skill - identify all AI-generated patterns
2. Color Palette Refinement skill - improve colors (professional SaaS style)
3. Typography System Design skill - create proper hierarchy
4. Spacing System Optimization skill - fix uniform spacing
5. Component State Enhancement skill - add all interactive states
6. Accessibility Audit skill - WCAG AA compliance
7. Next.js Optimization skill - optimize for Next.js 13+
8. Component Polish Pass skill - final polish

Component code:
[paste code]

Provide before/after comparison and explain each change.
```

---

## Creating Custom Skill Combinations

You can create your own workflows by combining skills:

```
Create a custom skill workflow for improving a dashboard page:
1. Analyze the page for AI patterns
2. Redesign the layout with intentional asymmetry
3. Refine the color palette for a fintech brand
4. Add professional micro-interactions
5. Ensure complete accessibility
6. Optimize for Next.js performance

[paste dashboard code]
```

---

## Conclusion

These skills provide a systematic approach to improving AI-generated UIs. They can be used individually for targeted improvements or chained together for comprehensive transformations. Each skill focuses on a specific aspect of professional design, making it easier to create polished, production-ready interfaces.
