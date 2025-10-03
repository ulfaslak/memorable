# UI/UX Design Specifications

> **Purpose:** Define the design system, user experience flows, and interface guidelines.

---

## Design System

### Color Palette

#### Primary Colors
```css
--primary-50: #...
--primary-100: #...
--primary-500: #...  /* Main brand color */
--primary-900: #...
```

#### Secondary Colors
```css
--secondary-50: #...
--secondary-500: #...
--secondary-900: #...
```

#### Semantic Colors
```css
--success: #...
--warning: #...
--error: #...
--info: #...
```

#### Neutral Colors
```css
--gray-50: #...    /* Backgrounds */
--gray-100: #...
--gray-500: #...   /* Body text */
--gray-900: #...   /* Headings */
```

#### Usage Guidelines
- Use primary colors for CTAs and key actions
- Use secondary colors for supporting elements
- Use semantic colors consistently for status messages
- Maintain 4.5:1 contrast ratio for WCAG AA compliance

---

### Typography

#### Font Families
- **Headings:** [Font Name], sans-serif
- **Body:** [Font Name], sans-serif
- **Monospace:** [Font Name], monospace

#### Font Sizes
```css
--text-xs: 0.75rem;   /* 12px */
--text-sm: 0.875rem;  /* 14px */
--text-base: 1rem;    /* 16px */
--text-lg: 1.125rem;  /* 18px */
--text-xl: 1.25rem;   /* 20px */
--text-2xl: 1.5rem;   /* 24px */
--text-3xl: 1.875rem; /* 30px */
--text-4xl: 2.25rem;  /* 36px */
```

#### Font Weights
- **Regular:** 400
- **Medium:** 500
- **Semibold:** 600
- **Bold:** 700

#### Line Heights
- Headings: 1.2
- Body text: 1.5
- Small text: 1.4

---

### Spacing System

```css
--spacing-1: 0.25rem;  /* 4px */
--spacing-2: 0.5rem;   /* 8px */
--spacing-3: 0.75rem;  /* 12px */
--spacing-4: 1rem;     /* 16px */
--spacing-6: 1.5rem;   /* 24px */
--spacing-8: 2rem;     /* 32px */
--spacing-12: 3rem;    /* 48px */
--spacing-16: 4rem;    /* 64px */
```

**Usage:**
- Use 4px base unit for all spacing
- Maintain consistent padding/margin across similar components
- Use larger spacing (48px+) between major sections

---

### Border Radius

```css
--radius-sm: 0.25rem;  /* 4px - buttons, inputs */
--radius-md: 0.5rem;   /* 8px - cards, modals */
--radius-lg: 1rem;     /* 16px - large containers */
--radius-full: 9999px; /* Full rounded - pills, avatars */
```

---

### Shadows

```css
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
--shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);
```

---

## Component Guidelines

### Buttons

#### Variants
- **Primary:** Main actions (submit, save, create)
- **Secondary:** Alternative actions (cancel, back)
- **Outline:** Tertiary actions
- **Ghost:** Minimal actions
- **Danger:** Destructive actions (delete, remove)

#### Sizes
- **Small:** 32px height, 12px 16px padding
- **Medium:** 40px height, 14px 20px padding
- **Large:** 48px height, 16px 24px padding

#### States
- Default
- Hover: Slight color darkening
- Active: Further darkening
- Disabled: Reduced opacity (0.5), no pointer events
- Loading: Show spinner, disable interaction

#### Example
```tsx
<Button variant="primary" size="md" disabled={false}>
  Click Me
</Button>
```

---

### Inputs

#### Text Inputs
- Height: 40px (md), 48px (lg)
- Border: 1px solid --gray-300
- Border radius: --radius-sm
- Focus: Blue ring, 2px offset
- Error: Red border, error message below

#### Labels
- Position: Above input
- Font size: --text-sm
- Font weight: Medium (500)
- Margin bottom: --spacing-2

#### Error Messages
- Color: --error
- Font size: --text-sm
- Margin top: --spacing-1

---

### Cards

- Background: White
- Border: 1px solid --gray-200 (or none)
- Border radius: --radius-md
- Padding: --spacing-6
- Shadow: --shadow-sm (hover: --shadow-md)

---

### Modals

- Backdrop: rgba(0, 0, 0, 0.5)
- Max width: 500px (sm), 768px (md), 1024px (lg)
- Border radius: --radius-lg
- Padding: --spacing-8
- Animation: Fade in + slide up

---

### Navigation

#### Header
- Height: 64px
- Background: White
- Border bottom: 1px solid --gray-200
- Sticky position: top 0

#### Sidebar (if applicable)
- Width: 256px
- Background: --gray-50
- Collapsible on mobile

---

## Responsive Design

### Breakpoints

```css
--mobile: 640px
--tablet: 768px
--desktop: 1024px
--wide: 1280px
```

### Mobile-First Approach
- Design for mobile first
- Progressively enhance for larger screens
- Test on actual devices

### Responsive Patterns
- **Navigation:** Hamburger menu on mobile, full nav on desktop
- **Grids:** Stack on mobile, multi-column on desktop
- **Typography:** Smaller font sizes on mobile
- **Spacing:** Reduced spacing on mobile

---

## User Flows

### Authentication Flow

1. **Landing Page** → Login/Register buttons
2. **Login Page** → Email + Password → Dashboard
3. **Register Page** → User details → Email verification → Dashboard
4. **Forgot Password** → Email input → Check email → Reset password → Login

### Main User Flow

1. **Dashboard** → Overview of key metrics/actions
2. **[Feature 1]** → Main functionality
3. **[Feature 2]** → Secondary functionality
4. **Settings** → User preferences and account management

---

## Interaction Patterns

### Loading States
- **Page load:** Full page skeleton or spinner
- **Component load:** Skeleton within component
- **Button action:** Spinner inside button, disable interaction
- **Infinite scroll:** Spinner at bottom

### Empty States
- Icon or illustration
- Clear message explaining why it's empty
- CTA to add first item

### Error States
- Clear error message
- Explanation of what went wrong
- Action to resolve (retry, go back, contact support)

---

## Accessibility (WCAG AA Compliance)

### Color Contrast
- Normal text: 4.5:1 minimum
- Large text (18pt+): 3:1 minimum
- UI components: 3:1 minimum

### Keyboard Navigation
- All interactive elements focusable
- Visible focus indicators
- Logical tab order
- Escape key closes modals

### Screen Readers
- Semantic HTML (header, nav, main, footer)
- Alt text for all images
- ARIA labels for icon buttons
- Form labels properly associated

### Focus Management
- Focus trap in modals
- Focus returns after modal close
- Skip to main content link

---

## Animation & Transitions

### Principles
- Use animation to guide attention
- Keep animations subtle and fast (200-300ms)
- Respect prefers-reduced-motion

### Common Transitions
- **Fade in:** opacity 0 → 1
- **Slide in:** transform translateY(10px) → 0
- **Scale:** transform scale(0.95) → 1
- **Hover effects:** 150ms ease-in-out

---

## Iconography

### Icon Library
- **Library:** [e.g., Heroicons, Lucide, Material Icons]
- **Size:** 16px (sm), 20px (md), 24px (lg)
- **Stroke width:** 2px (or 1.5px)
- **Color:** Inherit or --gray-500

### Usage
- Use icons to support text, not replace it (exceptions: universal icons)
- Maintain consistent style across all icons
- Provide aria-labels for icon-only buttons

---

## Form Validation

### Inline Validation
- Validate on blur, not on every keystroke
- Show error state immediately
- Show success state for important fields
- Disable submit button until form is valid

### Error Messages
- Be specific about what's wrong
- Suggest how to fix it
- Keep messages concise

---

## Notes

- Consult this document before implementing any UI component
- Update this document when establishing new patterns
- Maintain consistency with design system tokens
- Test all components across breakpoints
- Verify accessibility compliance for all interactive elements

