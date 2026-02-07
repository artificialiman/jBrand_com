# PERFORMANCE WEAR DESIGN STYLE GUIDE
**"Gear for the Driven"**

## BRAND PHILOSOPHY

Drawing from elite performance brands:
- **Ten Thousand**: Purpose-built precision, athlete-tested authenticity
- **Gymshark**: Community-driven energy, accessible performance
- **5.11 Tactical**: Mission-ready durability, functional excellence
- **Alphalete**: Sculpting performance, elevated aesthetics
- **Barbell Apparel**: Athletic fit innovation, everyday versatility

## CORE DESIGN PRINCIPLES

### 1. PERFORMANCE-FIRST AESTHETICS
- Clean, bold typography that commands attention
- High-contrast color schemes for immediate visual impact
- Tactical precision in spacing and alignment
- Movement-inspired UI animations

### 2. iOS-NATIVE FEEL
- Smooth 60fps animations
- Native gesture support (swipe, pull-to-refresh)
- Haptic feedback integration points
- Safe area respect for notched displays

### 3. PROGRESSIVE DISCLOSURE
- Critical actions always visible
- Secondary options revealed on interaction
- Smart defaults reduce cognitive load
- Contextual help where needed

---

## COLOR SYSTEM

### PRIMARY PALETTE
```
Deep Black      #0A0A0A    Authority, premium quality
Accent Orange   #FF3B00    Energy, urgency, CTA
Tech Green      #00E5A0    Progress, success states
```

### SECONDARY PALETTE
```
Warning Yellow  #FFB800    Caution, low stock alerts
Error Red       #FF1744    Errors, validation failures  
Success Green   #00C853    Confirmations, completions
```

### NEUTRAL GRAYS
```
White           #FFFFFF    Clean backgrounds
Grey 100        #F5F5F7    iOS light surface
Grey 400        #8E8E93    Placeholder text
Grey 900        #1C1C1E    Dark mode backgrounds
```

### USAGE GUIDELINES
- **Black + Orange**: High-energy CTAs, limited drops
- **Black + White + Grey**: Product photography backgrounds
- **Tech Green**: Progress indicators, stock availability
- **Use sparingly**: Orange accent should pop, not overwhelm

---

## TYPOGRAPHY HIERARCHY

### DISPLAY FONTS (Heroes, Landing Pages)
**Primary**: Bebas Neue, Oswald, Druk Wide
- All caps for maximum impact
- Tight letter-spacing (-2% to -3%)
- Line height 0.9-1.0 for stacked headlines

### HEADING FONTS (Product Titles, Sections)
**Primary**: Work Sans, DM Sans
- Semi-bold to Bold weights (600-700)
- Letter-spacing normal to -1%
- Clear hierarchy through size scaling

### BODY FONTS (Product Descriptions, UI)
**Primary**: Inter Tight, Geist, System
- Regular to Medium weights (400-500)
- Optimized for readability at 16px base
- 1.6 line-height for body copy

### SPECIAL USE CASES
- **Product SKUs/Codes**: JetBrains Mono (monospace)
- **Price Tags**: Bold display font, oversized
- **Badges/Labels**: Uppercase, wide letter-spacing

### RESPONSIVE SCALING
```
Mobile:   Base 14px → Clamp headlines 2.5-4rem
Tablet:   Base 15px → Clamp headlines 3-5rem  
Desktop:  Base 16px → Clamp headlines 4-6rem
```

---

## COMPONENT LIBRARY

### BUTTONS

#### Primary Action Button
```css
Background: Black (#0A0A0A)
Text: White
Height: 48px (mobile touch target)
Padding: 12px 24px
Border-radius: 4px
Shadow: Elevated on hover
State: Scale 0.98 on press
```

#### Secondary Action Button
```css
Background: Transparent
Text: Black
Border: 2px solid black
Hover: Fill black, text white
Active: Slight inward scale
```

#### CTA Button (Shop Now, Buy, Add to Cart)
```css
Background: Orange (#FF3B00)
Text: White, bold
Shadow: Glow effect on hover
Animation: Pulse on page load (once)
```

### CARDS

#### Product Card
```
Aspect Ratio: 3:4 (portrait)
Image: Cover fit, 5% scale on hover
Badge: Top-left, "NEW" / "SALE" / "SOLD OUT"
Title: Bold, 20px
Price: Large, 24px bold
Hover: Lift 4px, shadow expand
```

#### Category Card
```
Full bleed image background
Gradient overlay: Bottom fade to black
Title: White, display font, bottom-aligned
Interaction: Slight zoom on image
```

### FORMS

#### Input Fields
```css
Height: 48px minimum (thumb-friendly)
Border: 2px solid grey-300
Focus: Orange border, subtle glow
Error: Red border, shake animation
Success: Green border, checkmark icon
```

#### Validation Messages
```
Position: Below field, left-aligned
Color: Red (error), Green (success)
Icon: Leading indicator
Font: 12px, medium weight
```

---

## NOTIFICATION PATTERNS

### Toast Notifications
```
Position: Top-right on desktop, top-center on mobile
Duration: 4 seconds default, 6s for errors
Animation: Slide in from right (desktop), top (mobile)
Dismiss: Swipe right or auto-dismiss
```

### Status Types
1. **Success**: Green background, checkmark icon
2. **Error**: Red background, alert icon
3. **Warning**: Yellow background, caution icon
4. **Info**: Grey background, info icon

### Content Structure
```
[Icon] Bold Title
       Normal weight description text
       [Optional CTA button]
```

---

## LOADING STATES

### Skeleton Screens (Preferred)
```css
Background: Grey gradient shimmer
Animation: 2s infinite linear sweep
Elements: Match final layout structure
Use for: Product grids, cart, profile
```

### Spinner (Fallback)
```css
Size: 40px diameter
Color: Orange or black
Animation: Smooth rotation
Use for: Button states, form submits
```

### Progress Bars
```css
Height: 4px
Background: Light grey
Fill: Orange gradient
Use for: Checkout steps, file uploads
```

---

## SPACING SYSTEM

Based on 4px grid:
```
--space-1:  4px   (tight elements)
--space-2:  8px   (text line spacing)
--space-3:  12px  (button padding)
--space-4:  16px  (standard gap)
--space-5:  24px  (section spacing)
--space-6:  32px  (card padding)
--space-7:  48px  (section breaks)
--space-8:  64px  (major sections)
--space-9:  96px  (hero padding)
--space-10: 128px (page sections)
```

### Layout Widths
```
Container:  1440px max
Content:    1120px (reading width)
Narrow:     768px (forms, text-heavy)
```

---

## ANIMATIONS & MICRO-INTERACTIONS

### Page Transitions
```css
Duration: 250-350ms
Easing: cubic-bezier(0.4, 0, 0.2, 1)
Type: Fade + slight upward movement
```

### Button Interactions
```css
Hover: 2px lift, shadow expand
Active: Return to base, ripple effect
Loading: Spinner replace text
Success: Checkmark animation
```

### Card Interactions
```css
Hover: 4px lift, scale image 1.05
Active: Slight press down
Loading: Skeleton state
```

### Image Loading
```css
Initial: Low-res blur placeholder
Loading: Fade in from 0 to 1 opacity
Duration: 300ms ease-out
```

---

## RESPONSIVE BREAKPOINTS

```css
Mobile:     < 768px   (Stack, full-width cards)
Tablet:     768-1024px (2-column grids)
Desktop:    1024-1440px (3-4 column grids)
Wide:       > 1440px  (Max container width)
```

### Mobile-Specific
- Minimum touch target: 48x48px
- Navigation: Bottom tab bar OR hamburger
- Forms: Single column, large inputs
- Buttons: Full-width primary actions

### Desktop-Specific
- Hover states active
- Multi-column layouts
- Sidebar filters/navigation
- Larger product imagery

---

## ACCESSIBILITY STANDARDS

### Color Contrast
- Text on background: Minimum 4.5:1 (WCAG AA)
- Large text (18pt+): Minimum 3:1
- UI components: 3:1 contrast

### Keyboard Navigation
- Tab order follows visual flow
- Focus indicators: 2px orange outline
- Skip links for main navigation
- Enter/Space activate buttons

### Screen Readers
- Alt text on all images
- ARIA labels on icons
- Form field labels explicit
- Status announcements for dynamic content

---

## IMAGERY GUIDELINES

### Product Photography
```
Background: Pure white (#FFFFFF) or lifestyle
Format: WebP primary, JPEG fallback
Resolution: 2x for retina displays
Aspect: 3:4 portrait, 16:9 landscape
```

### Hero Images
```
Minimum: 1920x1080 desktop, 1080x1920 mobile
Quality: High compression (WebP 80%)
Treatment: Gradient overlay for text readability
Content: Active lifestyle, performance moments
```

### Icons
```
Style: Outline or filled, consistent set
Size: 24x24px base (scale via CSS)
Format: SVG for scalability
Color: Inherit from context
```

---

## WHATSAPP INTEGRATION DESIGN

### Checkout Button
```css
Background: #25D366 (WhatsApp green)
Icon: WhatsApp logo left-aligned
Text: "Complete Order via WhatsApp"
Size: Prominent, full-width on mobile
Position: Bottom of cart summary
```

### Chat Widget (Optional)
```
Position: Bottom-right, fixed
Icon: WhatsApp green circle
Hover: Expand to "Chat with us"
Mobile: Subtle, doesn't block content
```

---

## PWA MANIFEST REQUIREMENTS

```json
{
  "name": "Gear for the Driven",
  "short_name": "GFTD",
  "theme_color": "#0A0A0A",
  "background_color": "#FFFFFF",
  "display": "standalone",
  "orientation": "portrait",
  "start_url": "/",
  "icons": [
    {
      "src": "icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

### iOS Meta Tags
```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

---

## PERFORMANCE BENCHMARKS

### Load Times
- First Contentful Paint: < 1.5s
- Time to Interactive: < 3.5s
- Largest Contentful Paint: < 2.5s

### Asset Optimization
- Images: WebP format, lazy load below fold
- CSS: Critical inline, deferred non-critical
- Fonts: Subset, preload display fonts
- JavaScript: Code-split by route

---

## CONTENT VOICE & TONE

### Headlines
- **Bold, direct commands**: "Push Harder"
- **Challenge-focused**: "Built for the Grind"
- **Performance promises**: "Zero Restriction Movement"

### Product Descriptions
- Lead with performance benefit
- Technical specs secondary
- Social proof (reviews) prominent
- Scarcity indicators ("Only 5 left")

### Microcopy
- **Buttons**: Action verbs ("Add", "Shop", "Train")
- **Errors**: Helpful, not blaming
- **Empty states**: Motivational, not dead-end
- **Success**: Celebratory, momentum-building

---

## METRIC TRACKING TOUCHPOINTS

### User Journey Analytics
1. **Landing**: Hero engagement, scroll depth
2. **Browse**: Category clicks, filter usage  
3. **Product**: Image views, variant selections
4. **Cart**: Add/remove events, abandonment
5. **Checkout**: WhatsApp click, completion rate

### Performance KPIs
- Page load times per route
- Image load performance
- Animation frame rates
- Form completion rates
- Error frequency and types

---

## BRAND IMPLEMENTATION CHECKLIST

- [ ] Logo files (SVG, PNG 1x/2x)
- [ ] Color palette exported (CSS vars, design tokens)
- [ ] Typography loaded (Google Fonts / self-hosted)
- [ ] Icon library selected (Heroicons, Phosphor, etc.)
- [ ] Component library built (buttons, cards, forms)
- [ ] Animation library chosen (Framer Motion, GSAP, CSS)
- [ ] Notification system implemented
- [ ] Loading states designed (skeletons, spinners)
- [ ] Error states handled (404, 500, validation)
- [ ] PWA manifest configured
- [ ] iOS meta tags added
- [ ] WhatsApp integration tested
- [ ] Accessibility audit completed
- [ ] Performance benchmarks met

---

**Last Updated**: February 2026  
**Version**: 1.0  
**Maintained By**: Design Team
