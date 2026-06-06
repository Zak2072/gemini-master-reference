---
name: landing-page-generator
description: "Generates a premium, 3D-animated single-page HTML landing page from a text prompt, brief, or attached document. Use whenever the user says 'create a landing page', 'build a landing page', 'make a landing page for X', 'I need a web page for Y', 'one-pager', 'sales page', 'web presence', or 'promotional page'. Always use this skill rather than generating HTML ad hoc — it applies the full brand system and animation stack that makes the result genuinely impressive."
---

# Landing Page Generator

Creates a polished, self-contained HTML landing page with 3D CSS animations, GSAP ScrollTrigger scroll effects, and mouse-parallax panning. One brief in, one `.html` file out.

## Step 1: Content Extraction

Before writing a single line of HTML, identify these from the prompt or any attached file:

| Field | What to extract | Fallback if missing |
|---|---|---|
| **Product name** | The thing being promoted | Use the brand name |
| **Hero headline** | Short, punchy — ideally ≤8 words | Write a sharp one from context |
| **Hero subtext** | 1–2 sentence description | Write it from context |
| **Features / benefits** | 3–6 items, each with a title and 1-sentence description | Derive from context |
| **Primary CTA text** | Button label | "Get Started" |
| **Closing headline** | Big final push line | Riff on the hero headline |

If the input is a file, read it fully before generating.

## Step 2: Build the Page

The page has three required sections in a single self-contained HTML file.

### Section 1 — Hero

Full viewport height (`100vh`), Deep Navy background. Content centred vertically and horizontally.

**Structure (top to bottom):**
1. Optional eyebrow label (small, Teal, letter-spaced caps)
2. H1 headline — large, bold, Off-White
3. Subtitle paragraph — 1–2 sentences, muted Off-White
4. CTA button — Teal background, Navy text
5. Scroll-down indicator — subtle animated chevron at bottom centre

**Background depth layers** (`position: absolute`, `pointer-events: none`, `overflow: hidden` on the hero container):

Layer `.hero-shapes-back` (moves most on mouse):
- Large outlined rectangle: `340×200px`, `border: 2px solid rgba(0,212,170,0.12)`, `border-radius: 12px`, positioned `top: 12%; right: 7%`
- Small filled circle: `70×70px`, `border-radius: 50%`, `background: rgba(0,212,170,0.07)`, positioned `bottom: 22%; left: 8%`

Layer `.hero-shapes-mid` (moves less on mouse):
- Rotated square (diamond): `55×55px`, `background: rgba(245,166,35,0.18)`, `transform: rotate(45deg)`, positioned `top: 58%; right: 16%`
- Teal accent dot: `10×10px`, `border-radius: 50%`, `background: #00D4AA`, positioned `top: 28%; left: 7%`

Apply floating keyframe animations to shapes.

### Section 2 — Features

Background: `#0D1F38` (dark, slightly lighter than hero) unless the content feels especially light or consumer-facing, in which case use `#F7F7F2` (Off-White).

**Structure:**
1. Centred section headline (H2) — Inter 700, Off-White
2. Optional centred section subtext — 1 sentence
3. Grid of feature cards — 3 columns by default; 2 columns if exactly 4 features

**Feature card anatomy:**
```
[SVG icon — 28px, Teal stroke]
[Card title — Inter 600, 22px]
[Card description — Inter 400, 15px, muted]
```

Draw simple geometric SVG icons inline — match the card's concept. No icon font needed.

### Section 3 — Closing CTA

Full-width, Deep Navy. Centred layout.

**Structure:**
1. Large closing headline — Inter 800, 52–62px, Off-White
2. Short subtext — 1 sentence
3. CTA button (same style as hero)
4. Ambient glow behind button: `radial-gradient(ellipse 400px 200px at 50% 50%, rgba(0,212,170,0.12), transparent)`

## Brand System

### Colours
```css
--navy: #0A1628;
--navy-mid: #0D1F38;
--teal: #00D4AA;
--teal-glow: rgba(0, 212, 170, 0.12);
--amber: #F5A623;
--off-white: #F7F7F2;
--text-muted: rgba(247, 247, 242, 0.68);
--card-bg: rgba(0, 212, 170, 0.06);
--card-border: rgba(0, 212, 170, 0.15);
```

### Typography
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

## Step 3: Interactive Elements

Apply premium styling without external bloat:

- **Floating Shapes**: CSS keyframes (not heavy libraries) for ambient floating decorative shapes
- **Scroll Effects**: Simple entrance animations for text blocks as they enter the viewport
- **Mouse Parallax**: Subtle depth shift on hero background layers tracking mouse position

## Step 4: Output

- Provide the full code in the chat as a single `.html` file
- Offer to save the file to a location of the user's choice

## Principles

- **Grounding First**: Use the exact terminology and value propositions from the user's documents; never invent marketing fluff.
- **Strict Writing**: All text on the landing page must obey the Text DNA skill rules — British spelling, no em dashes, no AI slop verbs.
- **Directness**: The design should be high-conversion and focused on one specific action.
