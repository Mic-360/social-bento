---
name: material3-expressive-web
description: Expert guidance for building Material 3 Expressive websites and web apps using Astro and React. Use when creating web projects with M3 Expressive design: expressive color systems, springy motion, shape-based hierarchy, dynamic typography, component libraries (button groups, FABs, split buttons, navigation), and emotionally engaging UI. Covers Tailwind CSS integration, CSS custom properties for M3 tokens, React component patterns, and Astro island architecture for M3E sites.
metadata:
  author: bhaumic
  version: "0.0.1"
  argument-hint: <file-or-pattern>
---

# Material 3 Expressive Web (Astro + React)

Build emotionally engaging, modern web experiences using Material 3 Expressive design principles — adapted for Astro static sites and React web apps.

## Overview

Material 3 Expressive (M3E) is Google's most research-backed design evolution, proven to help users find key actions 4x faster and rate interfaces as more "energetic," "creative," "playful," and "friendly." On the web, M3E requires translating Flutter-native concepts (springs, shape morphing, dynamic color) into CSS, React, and Astro patterns.

**Five M3 Expressive Pillars for the Web:**
1. **Color with Purpose** — Seed-based palettes, vibrant on-container colors, attention-directing hues
2. **Shape Flexibility** — Rounded containers, morphing borders, pill shapes, shape-based visual hierarchy
3. **Size-Based Hierarchy** — Large hero elements, variable component sizing to show importance
4. **Springy Motion** — Physics-inspired CSS transitions and JS animations (not linear easings)
5. **Containment** — Surface elevations, card groupings, visual boundaries

---

## Design Thinking First

Before writing any code, commit to an expressive direction:

- **What emotion should this surface?** (playful / warm / dynamic / trustworthy)
- **Seed color** — Choose one bold seed; generate the full tonal palette from it
- **Shape language** — Pill-heavy (full rounding) vs. squircle vs. mixed organic shapes
- **Motion intensity** — Subtle spring feedback vs. bold morphing transitions
- **Typography contrast** — Expressive display fonts paired with readable body fonts

**CRITICAL**: M3E is intentional expressiveness, not decoration. Every bold choice should serve user comprehension or emotional connection.

---

## Tooling Setup

### Recommended Stack

| Tool | Role |
|------|------|
| Astro 4+ | Static/SSR framework, island architecture |
| React 18+ | Interactive component islands |
| Tailwind CSS 3+ | Utility classes + CSS variable bridge |
| Material Color Utilities | Seed-to-palette generation |
| Framer Motion | Springy animations in React |
| CSS Custom Properties | M3 design token system |

### Install Material Color Utilities

```bash
npm install @material/material-color-utilities
# Optional animation library
npm install framer-motion
```

### CSS Token System (tokens.css)

Define the full M3 token layer as CSS custom properties. Import globally in Astro's `Layout.astro` or React's root.

```css
/* tokens.css — M3 Expressive Design Tokens */
:root {
  /* === CORE PALETTE (generated from seed) === */
  --md-sys-color-primary: #6750A4;
  --md-sys-color-on-primary: #FFFFFF;
  --md-sys-color-primary-container: #EADDFF;
  --md-sys-color-on-primary-container: #21005D;

  --md-sys-color-secondary: #625B71;
  --md-sys-color-on-secondary: #FFFFFF;
  --md-sys-color-secondary-container: #E8DEF8;
  --md-sys-color-on-secondary-container: #1D192B;

  --md-sys-color-tertiary: #7D5260;
  --md-sys-color-on-tertiary: #FFFFFF;
  --md-sys-color-tertiary-container: #FFD8E4;
  --md-sys-color-on-tertiary-container: #31111D;

  --md-sys-color-error: #B3261E;
  --md-sys-color-on-error: #FFFFFF;
  --md-sys-color-error-container: #F9DEDC;
  --md-sys-color-on-error-container: #410E0B;

  --md-sys-color-surface: #FEF7FF;
  --md-sys-color-on-surface: #1C1B1F;
  --md-sys-color-surface-variant: #E7E0EC;
  --md-sys-color-on-surface-variant: #49454F;
  --md-sys-color-outline: #79747E;
  --md-sys-color-outline-variant: #CAC4D0;

  --md-sys-color-surface-container-lowest: #FFFFFF;
  --md-sys-color-surface-container-low: #F7F2FA;
  --md-sys-color-surface-container: #F3EDF7;
  --md-sys-color-surface-container-high: #ECE6F0;
  --md-sys-color-surface-container-highest: #E6E0E9;

  --md-sys-color-inverse-surface: #313033;
  --md-sys-color-inverse-on-surface: #F4EFF4;
  --md-sys-color-inverse-primary: #D0BCFF;

  /* === SHAPE TOKENS === */
  --md-sys-shape-corner-none: 0px;
  --md-sys-shape-corner-extra-small: 4px;
  --md-sys-shape-corner-small: 8px;
  --md-sys-shape-corner-medium: 12px;
  --md-sys-shape-corner-large: 16px;
  --md-sys-shape-corner-extra-large: 28px;
  --md-sys-shape-corner-full: 9999px;

  /* === ELEVATION (box-shadow) === */
  --md-sys-elevation-1: 0 1px 2px rgba(0,0,0,.3), 0 1px 3px 1px rgba(0,0,0,.15);
  --md-sys-elevation-2: 0 1px 2px rgba(0,0,0,.3), 0 2px 6px 2px rgba(0,0,0,.15);
  --md-sys-elevation-3: 0 4px 8px 3px rgba(0,0,0,.15), 0 1px 3px rgba(0,0,0,.3);
  --md-sys-elevation-4: 0 6px 10px 4px rgba(0,0,0,.15), 0 2px 3px rgba(0,0,0,.3);

  /* === MOTION TOKENS === */
  --md-sys-motion-easing-standard: cubic-bezier(0.2, 0, 0, 1);
  --md-sys-motion-easing-standard-decelerate: cubic-bezier(0, 0, 0, 1);
  --md-sys-motion-easing-standard-accelerate: cubic-bezier(0.3, 0, 1, 1);
  --md-sys-motion-easing-emphasized: cubic-bezier(0.2, 0, 0, 1);
  --md-sys-motion-easing-spring: cubic-bezier(0.175, 0.885, 0.32, 1.275);

  --md-sys-motion-duration-short1: 50ms;
  --md-sys-motion-duration-short2: 100ms;
  --md-sys-motion-duration-short3: 150ms;
  --md-sys-motion-duration-short4: 200ms;
  --md-sys-motion-duration-medium1: 250ms;
  --md-sys-motion-duration-medium2: 300ms;
  --md-sys-motion-duration-medium3: 350ms;
  --md-sys-motion-duration-medium4: 400ms;
  --md-sys-motion-duration-long1: 450ms;
  --md-sys-motion-duration-long2: 500ms;

  /* === TYPOGRAPHY === */
  --md-sys-typescale-display-large-size: 57px;
  --md-sys-typescale-display-large-weight: 400;
  --md-sys-typescale-display-large-tracking: -0.25px;
  --md-sys-typescale-headline-large-size: 32px;
  --md-sys-typescale-headline-medium-size: 28px;
  --md-sys-typescale-headline-small-size: 24px;
  --md-sys-typescale-title-large-size: 22px;
  --md-sys-typescale-body-large-size: 16px;
  --md-sys-typescale-body-medium-size: 14px;
  --md-sys-typescale-label-large-size: 14px;
  --md-sys-typescale-label-large-weight: 500;
}

/* Dark scheme override */
[data-theme="dark"] {
  --md-sys-color-primary: #D0BCFF;
  --md-sys-color-on-primary: #381E72;
  --md-sys-color-primary-container: #4F378B;
  --md-sys-color-on-primary-container: #EADDFF;
  --md-sys-color-surface: #141218;
  --md-sys-color-on-surface: #E6E0E9;
  --md-sys-color-surface-container: #211F26;
  /* ... extend for full dark palette */
}
```

---

## Dynamic Color Generation (from Seed)

Generate a full M3 tonal palette from any seed color at runtime or build time.

```ts
// lib/m3-theme.ts
import {
  argbFromHex,
  themeFromSourceColor,
  applyTheme,
} from "@material/material-color-utilities";

export function applyM3Theme(seedHex: string, isDark = false) {
  const theme = themeFromSourceColor(argbFromHex(seedHex));
  applyTheme(theme, { target: document.documentElement, dark: isDark });
}

// Usage in React island or Astro script:
// applyM3Theme("#6750A4", false);
```

### Astro Integration (Layout.astro)

```astro
---
// src/layouts/Layout.astro
import "../styles/tokens.css";
---
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <slot name="head" />
  </head>
  <body style="background: var(--md-sys-color-surface); color: var(--md-sys-color-on-surface);">
    <slot />
    <script>
      import { applyM3Theme } from "../lib/m3-theme";
      const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
      applyM3Theme("#6750A4", prefersDark);
      document.documentElement.setAttribute("data-theme", prefersDark ? "dark" : "light");
    </script>
  </body>
</html>
```

---

## Component Library

### 1. Buttons

M3E buttons use emphasized shapes (pill/full rounding), larger touch targets, and springy state responses.

```tsx
// components/Button.tsx
import { motion } from "framer-motion";

type ButtonVariant = "filled" | "tonal" | "outlined" | "text" | "elevated";
type ButtonSize = "sm" | "md" | "lg" | "xl";

const sizeStyles: Record<ButtonSize, string> = {
  sm: "h-8 px-4 text-sm",
  md: "h-10 px-6 text-sm",
  lg: "h-12 px-8 text-base",
  xl: "h-14 px-10 text-lg",
};

const variantStyles: Record<ButtonVariant, string> = {
  filled:   "bg-[var(--md-sys-color-primary)] text-[var(--md-sys-color-on-primary)]",
  tonal:    "bg-[var(--md-sys-color-secondary-container)] text-[var(--md-sys-color-on-secondary-container)]",
  outlined: "border border-[var(--md-sys-color-outline)] text-[var(--md-sys-color-primary)] bg-transparent",
  text:     "text-[var(--md-sys-color-primary)] bg-transparent",
  elevated: "bg-[var(--md-sys-color-surface-container-low)] text-[var(--md-sys-color-primary)] shadow-md",
};

interface ButtonProps {
  variant?: ButtonVariant;
  size?: ButtonSize;
  icon?: React.ReactNode;
  children: React.ReactNode;
  onClick?: () => void;
  disabled?: boolean;
}

export function Button({
  variant = "filled",
  size = "md",
  icon,
  children,
  onClick,
  disabled,
}: ButtonProps) {
  return (
    <motion.button
      onClick={onClick}
      disabled={disabled}
      whileTap={{ scale: 0.95 }}
      whileHover={{ scale: 1.02 }}
      transition={{ type: "spring", stiffness: 400, damping: 17 }}
      className={[
        "inline-flex items-center gap-2 font-medium rounded-full cursor-pointer select-none",
        "transition-all duration-200 outline-none",
        "focus-visible:ring-2 focus-visible:ring-[var(--md-sys-color-primary)] focus-visible:ring-offset-2",
        "disabled:opacity-38 disabled:cursor-not-allowed",
        sizeStyles[size],
        variantStyles[variant],
      ].join(" ")}
    >
      {icon && <span className="w-[1.125em] h-[1.125em]">{icon}</span>}
      {children}
    </motion.button>
  );
}
```

### 2. Button Groups

Segmented/toggle button groups — new in M3E.

```tsx
// components/ButtonGroup.tsx
import { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";

interface SegmentedButtonOption {
  value: string;
  label: string;
  icon?: React.ReactNode;
}

interface SegmentedButtonGroupProps {
  options: SegmentedButtonOption[];
  defaultValue?: string;
  multiSelect?: boolean;
  onChange?: (value: string | string[]) => void;
}

export function SegmentedButtonGroup({
  options,
  defaultValue,
  multiSelect = false,
  onChange,
}: SegmentedButtonGroupProps) {
  const [selected, setSelected] = useState<string[]>(
    defaultValue ? [defaultValue] : []
  );

  const toggle = (value: string) => {
    let next: string[];
    if (multiSelect) {
      next = selected.includes(value)
        ? selected.filter((v) => v !== value)
        : [...selected, value];
    } else {
      next = selected[0] === value ? [] : [value];
    }
    setSelected(next);
    onChange?.(multiSelect ? next : next[0] ?? "");
  };

  return (
    <div
      role="group"
      className="inline-flex overflow-hidden border border-[var(--md-sys-color-outline)] rounded-full"
    >
      {options.map((opt, i) => {
        const isSelected = selected.includes(opt.value);
        return (
          <motion.button
            key={opt.value}
            onClick={() => toggle(opt.value)}
            whileTap={{ scale: 0.96 }}
            transition={{ type: "spring", stiffness: 500, damping: 20 }}
            className={[
              "relative h-10 px-4 text-sm font-medium flex items-center gap-2 cursor-pointer select-none",
              "transition-colors duration-200",
              i > 0 ? "border-l border-[var(--md-sys-color-outline)]" : "",
              isSelected
                ? "bg-[var(--md-sys-color-secondary-container)] text-[var(--md-sys-color-on-secondary-container)]"
                : "bg-transparent text-[var(--md-sys-color-on-surface)]",
            ].join(" ")}
          >
            {opt.icon && <span className="w-4 h-4">{opt.icon}</span>}
            <AnimatePresence>
              {isSelected && (
                <motion.span
                  initial={{ width: 0, opacity: 0 }}
                  animate={{ width: "auto", opacity: 1 }}
                  exit={{ width: 0, opacity: 0 }}
                  transition={{ type: "spring", stiffness: 400, damping: 25 }}
                  className="overflow-hidden"
                >
                  ✓{" "}
                </motion.span>
              )}
            </AnimatePresence>
            {opt.label}
          </motion.button>
        );
      })}
    </div>
  );
}
```

### 3. Cards

M3E cards use surface containers, shape-based containment, and subtle elevation.

```tsx
// components/Card.tsx
import { motion } from "framer-motion";

type CardVariant = "elevated" | "filled" | "outlined";

interface CardProps {
  variant?: CardVariant;
  interactive?: boolean;
  className?: string;
  children: React.ReactNode;
  onClick?: () => void;
}

const variantStyles: Record<CardVariant, string> = {
  elevated: "bg-[var(--md-sys-color-surface-container-low)] shadow-[var(--md-sys-elevation-1)]",
  filled:   "bg-[var(--md-sys-color-surface-container-highest)]",
  outlined: "bg-[var(--md-sys-color-surface)] border border-[var(--md-sys-color-outline-variant)]",
};

export function Card({ variant = "elevated", interactive = false, className = "", children, onClick }: CardProps) {
  const Component = interactive ? motion.div : "div";
  const motionProps = interactive
    ? {
        whileHover: { y: -2, boxShadow: "var(--md-sys-elevation-2)" },
        whileTap: { scale: 0.98 },
        transition: { type: "spring", stiffness: 400, damping: 20 },
      }
    : {};

  return (
    <Component
      onClick={onClick}
      {...motionProps}
      className={[
        "rounded-[var(--md-sys-shape-corner-large)] overflow-hidden",
        "transition-shadow duration-300",
        interactive ? "cursor-pointer" : "",
        variantStyles[variant],
        className,
      ].join(" ")}
    >
      {children}
    </Component>
  );
}
```

### 4. FAB (Floating Action Button) with Menu

```tsx
// components/FABMenu.tsx
import { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";

interface FABAction {
  icon: React.ReactNode;
  label: string;
  onClick: () => void;
}

interface FABMenuProps {
  primaryIcon: React.ReactNode;
  actions: FABAction[];
  size?: "sm" | "md" | "lg";
}

export function FABMenu({ primaryIcon, actions, size = "md" }: FABMenuProps) {
  const [open, setOpen] = useState(false);

  const fabSize = { sm: "w-10 h-10", md: "w-14 h-14", lg: "w-24 h-24" }[size];

  return (
    <div className="fixed bottom-6 right-6 flex flex-col-reverse items-end gap-3">
      {/* Mini FABs */}
      <AnimatePresence>
        {open &&
          actions.map((action, i) => (
            <motion.div
              key={i}
              initial={{ opacity: 0, y: 20, scale: 0.8 }}
              animate={{ opacity: 1, y: 0, scale: 1 }}
              exit={{ opacity: 0, y: 20, scale: 0.8 }}
              transition={{
                type: "spring",
                stiffness: 400,
                damping: 25,
                delay: i * 0.05,
              }}
              className="flex items-center gap-3"
            >
              <span className="bg-[var(--md-sys-color-surface-container-high)] text-[var(--md-sys-color-on-surface)] px-3 py-1.5 rounded-full text-sm shadow-md whitespace-nowrap">
                {action.label}
              </span>
              <motion.button
                onClick={() => { action.onClick(); setOpen(false); }}
                whileTap={{ scale: 0.9 }}
                className="w-10 h-10 rounded-full bg-[var(--md-sys-color-secondary-container)] text-[var(--md-sys-color-on-secondary-container)] flex items-center justify-center shadow-[var(--md-sys-elevation-2)]"
              >
                {action.icon}
              </motion.button>
            </motion.div>
          ))}
      </AnimatePresence>

      {/* Primary FAB */}
      <motion.button
        onClick={() => setOpen(!open)}
        whileHover={{ scale: 1.05 }}
        whileTap={{ scale: 0.92 }}
        animate={{ rotate: open ? 45 : 0 }}
        transition={{ type: "spring", stiffness: 400, damping: 20 }}
        className={[
          fabSize,
          "rounded-[var(--md-sys-shape-corner-large)] flex items-center justify-center",
          "bg-[var(--md-sys-color-primary-container)] text-[var(--md-sys-color-on-primary-container)]",
          "shadow-[var(--md-sys-elevation-3)] cursor-pointer",
        ].join(" ")}
      >
        {primaryIcon}
      </motion.button>
    </div>
  );
}
```

### 5. Navigation Bar (Bottom)

```tsx
// components/NavigationBar.tsx
import { motion } from "framer-motion";

interface NavItem {
  icon: React.ReactNode;
  activeIcon?: React.ReactNode;
  label: string;
  href?: string;
  badge?: number;
}

interface NavigationBarProps {
  items: NavItem[];
  activeIndex: number;
  onSelect?: (index: number) => void;
}

export function NavigationBar({ items, activeIndex, onSelect }: NavigationBarProps) {
  return (
    <nav className="fixed bottom-0 inset-x-0 bg-[var(--md-sys-color-surface-container)] border-t border-[var(--md-sys-color-outline-variant)] flex justify-around items-center h-20 px-2 z-50">
      {items.map((item, i) => {
        const isActive = i === activeIndex;
        return (
          <button
            key={i}
            onClick={() => onSelect?.(i)}
            className="flex-1 flex flex-col items-center gap-1 py-3 relative cursor-pointer"
          >
            {/* Active indicator pill */}
            <AnimatedPill active={isActive} />

            {/* Icon */}
            <motion.span
              animate={{ scale: isActive ? 1.1 : 1 }}
              transition={{ type: "spring", stiffness: 500, damping: 20 }}
              className="relative z-10 text-xl"
            >
              {isActive && item.activeIcon ? item.activeIcon : item.icon}
            </motion.span>

            {/* Badge */}
            {item.badge != null && (
              <span className="absolute top-2 right-[30%] bg-[var(--md-sys-color-error)] text-[var(--md-sys-color-on-error)] text-[10px] font-bold rounded-full w-4 h-4 flex items-center justify-center">
                {item.badge > 9 ? "9+" : item.badge}
              </span>
            )}

            <span
              className={`text-xs font-medium ${
                isActive
                  ? "text-[var(--md-sys-color-on-secondary-container)]"
                  : "text-[var(--md-sys-color-on-surface-variant)]"
              }`}
            >
              {item.label}
            </span>
          </button>
        );
      })}
    </nav>
  );
}

function AnimatedPill({ active }: { active: boolean }) {
  return (
    <motion.div
      animate={{
        width: active ? "4rem" : "0rem",
        opacity: active ? 1 : 0,
      }}
      transition={{ type: "spring", stiffness: 400, damping: 30 }}
      className="absolute top-2 h-8 rounded-full bg-[var(--md-sys-color-secondary-container)]"
    />
  );
}
```

### 6. Navigation Rail (Side)

```tsx
// components/NavigationRail.tsx
import { motion } from "framer-motion";

interface RailItem {
  icon: React.ReactNode;
  activeIcon?: React.ReactNode;
  label: string;
  badge?: number;
}

interface NavigationRailProps {
  items: RailItem[];
  activeIndex: number;
  onSelect?: (i: number) => void;
  fab?: React.ReactNode;
  onFabClick?: () => void;
}

export function NavigationRail({ items, activeIndex, onSelect, fab, onFabClick }: NavigationRailProps) {
  return (
    <nav className="fixed top-0 left-0 h-screen w-20 flex flex-col items-center pt-4 pb-6 gap-2 bg-[var(--md-sys-color-surface-container)] z-40">
      {fab && (
        <motion.button
          onClick={onFabClick}
          whileHover={{ scale: 1.05 }}
          whileTap={{ scale: 0.95 }}
          className="w-14 h-14 rounded-[var(--md-sys-shape-corner-large)] bg-[var(--md-sys-color-primary-container)] text-[var(--md-sys-color-on-primary-container)] flex items-center justify-center mb-4 shadow-[var(--md-sys-elevation-2)]"
        >
          {fab}
        </motion.button>
      )}

      {items.map((item, i) => {
        const isActive = i === activeIndex;
        return (
          <button
            key={i}
            onClick={() => onSelect?.(i)}
            className="flex flex-col items-center gap-1 w-full px-2 py-1 cursor-pointer"
          >
            <motion.div
              animate={{
                backgroundColor: isActive
                  ? "var(--md-sys-color-secondary-container)"
                  : "transparent",
                width: isActive ? "3.5rem" : "2rem",
              }}
              transition={{ type: "spring", stiffness: 400, damping: 28 }}
              className="h-8 rounded-full flex items-center justify-center text-xl overflow-hidden"
            >
              {isActive && item.activeIcon ? item.activeIcon : item.icon}
            </motion.div>
            <span
              className={`text-[10px] font-medium leading-tight text-center ${
                isActive
                  ? "text-[var(--md-sys-color-on-secondary-container)]"
                  : "text-[var(--md-sys-color-on-surface-variant)]"
              }`}
            >
              {item.label}
            </span>
          </button>
        );
      })}
    </nav>
  );
}
```

### 7. Loading Indicator (Wavy / Expressive)

M3E replaces flat spinners with organic, wavy progress indicators.

```tsx
// components/LoadingIndicator.tsx
import { motion } from "framer-motion";

interface LoadingIndicatorProps {
  size?: "sm" | "md" | "lg";
  color?: string;
  type?: "circular" | "linear" | "wavy";
}

export function LoadingIndicator({
  size = "md",
  color = "var(--md-sys-color-primary)",
  type = "wavy",
}: LoadingIndicatorProps) {
  if (type === "wavy") {
    return <WavyLoader color={color} size={size} />;
  }
  if (type === "circular") {
    return <CircularLoader color={color} size={size} />;
  }
  return <LinearLoader color={color} />;
}

function WavyLoader({ color, size }: { color: string; size: string }) {
  const bars = 5;
  const heights = ["0.6rem", "1rem", "1.4rem", "1rem", "0.6rem"];
  const sizeClass = { sm: "h-6 gap-0.5", md: "h-10 gap-1", lg: "h-14 gap-1.5" }[size];
  return (
    <div className={`flex items-center ${sizeClass}`}>
      {Array.from({ length: bars }).map((_, i) => (
        <motion.div
          key={i}
          style={{ backgroundColor: color, height: heights[i] }}
          className="w-1.5 rounded-full"
          animate={{ scaleY: [1, 1.8, 1] }}
          transition={{
            duration: 0.8,
            repeat: Infinity,
            delay: i * 0.12,
            ease: "easeInOut",
          }}
        />
      ))}
    </div>
  );
}

function CircularLoader({ color, size }: { color: string; size: string }) {
  const dim = { sm: 24, md: 40, lg: 56 }[size];
  return (
    <motion.svg
      width={dim} height={dim} viewBox="0 0 40 40"
      animate={{ rotate: 360 }}
      transition={{ duration: 1.2, repeat: Infinity, ease: "linear" }}
    >
      <circle cx="20" cy="20" r="16" fill="none" stroke={color} strokeWidth="4" strokeLinecap="round" strokeDasharray="60 40" />
    </motion.svg>
  );
}

function LinearLoader({ color }: { color: string }) {
  return (
    <div className="w-full h-1 bg-[var(--md-sys-color-surface-variant)] rounded-full overflow-hidden">
      <motion.div
        className="h-full rounded-full"
        style={{ backgroundColor: color }}
        animate={{ x: ["-100%", "100%"] }}
        transition={{ duration: 1.4, repeat: Infinity, ease: "easeInOut" }}
      />
    </div>
  );
}
```

### 8. Split Button

```tsx
// components/SplitButton.tsx
import { useState, useRef, useEffect } from "react";
import { motion, AnimatePresence } from "framer-motion";

interface SplitButtonOption {
  label: string;
  onClick: () => void;
}

interface SplitButtonProps {
  primary: SplitButtonOption;
  options: SplitButtonOption[];
  variant?: "filled" | "tonal";
}

export function SplitButton({ primary, options, variant = "filled" }: SplitButtonProps) {
  const [open, setOpen] = useState(false);
  const ref = useRef<HTMLDivElement>(null);

  useEffect(() => {
    const handler = (e: MouseEvent) => {
      if (ref.current && !ref.current.contains(e.target as Node)) setOpen(false);
    };
    document.addEventListener("mousedown", handler);
    return () => document.removeEventListener("mousedown", handler);
  }, []);

  const baseStyle =
    variant === "filled"
      ? "bg-[var(--md-sys-color-primary)] text-[var(--md-sys-color-on-primary)]"
      : "bg-[var(--md-sys-color-secondary-container)] text-[var(--md-sys-color-on-secondary-container)]";

  return (
    <div ref={ref} className="relative inline-flex">
      {/* Primary action */}
      <motion.button
        whileTap={{ scale: 0.97 }}
        onClick={primary.onClick}
        className={`h-10 px-5 text-sm font-medium rounded-l-full cursor-pointer ${baseStyle}`}
      >
        {primary.label}
      </motion.button>

      {/* Divider + dropdown trigger */}
      <motion.button
        whileTap={{ scale: 0.97 }}
        onClick={() => setOpen(!open)}
        className={`h-10 w-8 flex items-center justify-center rounded-r-full border-l border-white/20 cursor-pointer ${baseStyle}`}
      >
        <motion.span animate={{ rotate: open ? 180 : 0 }} transition={{ type: "spring", stiffness: 400, damping: 20 }}>
          ▾
        </motion.span>
      </motion.button>

      {/* Dropdown */}
      <AnimatePresence>
        {open && (
          <motion.div
            initial={{ opacity: 0, y: -8, scale: 0.95 }}
            animate={{ opacity: 1, y: 0, scale: 1 }}
            exit={{ opacity: 0, y: -8, scale: 0.95 }}
            transition={{ type: "spring", stiffness: 400, damping: 25 }}
            className="absolute top-12 right-0 min-w-[10rem] bg-[var(--md-sys-color-surface-container)] rounded-[var(--md-sys-shape-corner-extra-large)] shadow-[var(--md-sys-elevation-2)] overflow-hidden z-50"
          >
            {options.map((opt, i) => (
              <button
                key={i}
                onClick={() => { opt.onClick(); setOpen(false); }}
                className="w-full text-left px-4 py-3 text-sm text-[var(--md-sys-color-on-surface)] hover:bg-[var(--md-sys-color-surface-container-highest)] transition-colors cursor-pointer"
              >
                {opt.label}
              </button>
            ))}
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
}
```

---

## Motion Guide

### M3E Spring Philosophy

M3E avoids `linear` and generic `ease-in-out`. Use physics springs:

```ts
// Framer Motion spring presets
export const springs = {
  // UI feedback: button press, toggle
  snappy:   { type: "spring", stiffness: 500, damping: 20 },
  // Navigation: page transitions, modals
  gentle:   { type: "spring", stiffness: 280, damping: 30 },
  // Expandable content: FAB menu, accordions
  bouncy:   { type: "spring", stiffness: 300, damping: 15 },
  // Subtle hover effects
  soft:     { type: "spring", stiffness: 200, damping: 25 },
};
```

### CSS-Only Spring (no library)

```css
.m3-interactive {
  transition:
    transform var(--md-sys-motion-duration-medium2) var(--md-sys-motion-easing-spring),
    box-shadow var(--md-sys-motion-duration-medium1) var(--md-sys-motion-easing-standard);
}

.m3-interactive:hover { transform: translateY(-2px); }
.m3-interactive:active { transform: scale(0.97); }
```

### Page Transitions (Astro View Transitions)

```astro
---
// Layout.astro
import { ViewTransitions } from "astro:transitions";
---
<head>
  <ViewTransitions />
</head>
```

```css
/* Custom M3E page transition */
::view-transition-old(root) {
  animation: 300ms var(--md-sys-motion-easing-standard-accelerate) fade-out;
}
::view-transition-new(root) {
  animation: 400ms var(--md-sys-motion-easing-standard-decelerate) fade-in-slide;
}

@keyframes fade-out {
  to { opacity: 0; transform: scale(0.98); }
}
@keyframes fade-in-slide {
  from { opacity: 0; transform: scale(1.02); }
}
```

### Reduced Motion

Always respect user preferences:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

```tsx
// React hook
import { useReducedMotion } from "framer-motion";

function MyComponent() {
  const reduced = useReducedMotion();
  const spring = reduced ? { type: "tween", duration: 0.01 } : springs.snappy;
  // ...
}
```

---

## Astro Architecture Patterns

### Astro + React Island

Keep static Astro shells for SEO/performance; hydrate only interactive M3E components.

```astro
---
// src/pages/index.astro
import Layout from "../layouts/Layout.astro";
import { NavigationBar } from "../components/NavigationBar";
import { FABMenu } from "../components/FABMenu";
---

<Layout>
  <!-- Static Astro content (no JS) -->
  <main class="ml-0 md:ml-20 pb-20 md:pb-0">
    <slot />
  </main>

  <!-- Hydrated React islands -->
  <NavigationBar client:load items={navItems} activeIndex={0} />
  <FABMenu client:visible primaryIcon="+" actions={fabActions} />
</Layout>
```

### Hydration Strategy

| Component | Directive | Reason |
|-----------|-----------|--------|
| Navigation | `client:load` | Always visible, immediate |
| FAB | `client:visible` | Below fold, defer |
| Dialogs/Modals | `client:idle` | Triggered by user |
| Charts/Heavy UI | `client:only="react"` | No SSR needed |

---

## Tailwind Integration

Bridge Tailwind with M3 tokens via `tailwind.config.js`:

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        "md-primary":           "var(--md-sys-color-primary)",
        "md-on-primary":        "var(--md-sys-color-on-primary)",
        "md-primary-container": "var(--md-sys-color-primary-container)",
        "md-secondary":         "var(--md-sys-color-secondary)",
        "md-surface":           "var(--md-sys-color-surface)",
        "md-on-surface":        "var(--md-sys-color-on-surface)",
        "md-surface-container": "var(--md-sys-color-surface-container)",
        "md-outline":           "var(--md-sys-color-outline)",
        "md-error":             "var(--md-sys-color-error)",
      },
      borderRadius: {
        "md-sm":  "var(--md-sys-shape-corner-small)",
        "md-md":  "var(--md-sys-shape-corner-medium)",
        "md-lg":  "var(--md-sys-shape-corner-large)",
        "md-xl":  "var(--md-sys-shape-corner-extra-large)",
        "md-full":"var(--md-sys-shape-corner-full)",
      },
      boxShadow: {
        "md-1": "var(--md-sys-elevation-1)",
        "md-2": "var(--md-sys-elevation-2)",
        "md-3": "var(--md-sys-elevation-3)",
      },
    },
  },
};
```

---

## Typography

M3E typography uses expressive, size-driven hierarchy. Pair a characterful display font with a clean body font.

```css
/* Good M3E web font pairings */

/* Option A: Warm & Playful */
@import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;800&family=Plus+Jakarta+Sans:wght@400;500;600&display=swap');

/* Option B: Editorial & Bold */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@400;500&display=swap');

/* Option C: Modern Geometric */
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700&family=Lato:wght@400;700&display=swap');

:root {
  --md-ref-typeface-brand: "Nunito", sans-serif;    /* display/headline */
  --md-ref-typeface-plain: "Plus Jakarta Sans", sans-serif; /* body/label */
}

.md-display-large {
  font-family: var(--md-ref-typeface-brand);
  font-size: var(--md-sys-typescale-display-large-size);
  font-weight: 700;
  letter-spacing: var(--md-sys-typescale-display-large-tracking);
  line-height: 1.12;
}

.md-headline-large {
  font-family: var(--md-ref-typeface-brand);
  font-size: var(--md-sys-typescale-headline-large-size);
  font-weight: 600;
  line-height: 1.2;
}

.md-body-large {
  font-family: var(--md-ref-typeface-plain);
  font-size: var(--md-sys-typescale-body-large-size);
  line-height: 1.5;
}
```

---

## Color Strategy

### Generating Palettes

Use [Material Theme Builder](https://material-foundation.github.io/material-theme-builder/) or the JS library to generate from any seed:

```ts
// scripts/generate-tokens.ts
import { argbFromHex, themeFromSourceColor } from "@material/material-color-utilities";
import fs from "fs";

const seed = "#00897B"; // Your brand seed
const theme = themeFromSourceColor(argbFromHex(seed));
const scheme = theme.schemes.light;

const tokens = `
:root {
  --md-sys-color-primary: ${hexFromArgb(scheme.primary)};
  --md-sys-color-on-primary: ${hexFromArgb(scheme.onPrimary)};
  /* ... */
}
`;
fs.writeFileSync("src/styles/generated-tokens.css", tokens);
```

### M3E Color Principles for Web

- Use **primary** for the single most important CTA per page
- Use **secondary-container** for active navigation states (not primary — too heavy)
- Use **tertiary** sparingly, for accent/decorative moments
- Use **surface containers** (lowest → highest) for layered elevation without shadows on mobile
- Avoid pure black/white; always use `on-surface` / `surface` tokens

---

## Accessibility

M3E's expressive colors must still meet WCAG 2.1:

```tsx
// Utility: Check M3 token contrast
export function m3ContrastCheck(fg: string, bg: string): boolean {
  // Use a contrast checker (e.g. colorjs.io) with your token hex values
  // M3 guarantees contrast for official on-color pairs (on-primary vs primary)
  // Custom combinations MUST be checked
  return true; // replace with real check
}
```

**Guidelines:**
- All `on-*` / `*` pairs in the M3 spec meet WCAG AA by design — use them as intended
- Never put `primary` text on `secondary-container` backgrounds without checking
- Minimum touch target: 48x48px (use padding to extend small visual elements)
- Focus rings: always visible via `focus-visible`, use `--md-sys-color-primary` ring

---

## Recommended Workflow

### Phase 1: Design Foundation
1. Choose a seed color that matches the brand or emotion
2. Generate full M3 palette via Material Theme Builder or CLI script
3. Decide on shape language (pill-heavy vs. rounded-lg for less playful)
4. Pick typography pairing (expressive display + clean body)
5. Plan motion intensity (subtle vs. bold springs)

### Phase 2: Astro Project Setup
1. Create Astro project with React integration: `npx create astro@latest --template minimal`
2. Add React: `npx astro add react`
3. Add Tailwind: `npx astro add tailwind`
4. Install dependencies: `npm install @material/material-color-utilities framer-motion`
5. Create `src/styles/tokens.css`, import in `Layout.astro`
6. Configure `tailwind.config.js` with M3 token bridge

### Phase 3: Component Build
1. Start with tokens + `Layout.astro`
2. Build `Button`, `Card`, `NavigationBar` (most used)
3. Add `FABMenu`, `LoadingIndicator`, `SegmentedButtonGroup` as needed
4. Apply Astro `client:*` directives for appropriate hydration

### Phase 4: Polish
1. Test all spring animations at 60fps in Chrome DevTools
2. Validate color contrast with browser accessibility tools
3. Enable `prefers-reduced-motion` CSS
4. Test dark/light theme switching
5. Validate Astro View Transitions for page animations

---

## Best Practices

1. **Token-first** — Never hardcode colors or radius values; always use CSS custom properties
2. **Springs, not linear** — Replace all `ease-in-out` with `cubic-bezier` spring curves or Framer Motion springs
3. **Island sparingly** — Keep Astro pages mostly static; only hydrate genuinely interactive M3E components
4. **One primary CTA per view** — M3E's color purposefulness means primary should guide attention to one thing
5. **Size creates hierarchy** — Make important content larger, not just bolder; M3E uses size as a primary signal
6. **Test on real devices** — Springs feel fundamentally different on mobile hardware than in browser devtools
7. **Dark mode from the start** — Build both schemes simultaneously; retrofitting dark mode is painful with M3 tokens
8. **Accessibility is non-negotiable** — M3E's expressiveness must not compromise WCAG compliance

---

## Quick Reference

| Task | Component / File |
|------|-----------------|
| Set up M3 tokens | `tokens.css` |
| Generate palette from seed | `lib/m3-theme.ts` |
| Filled / tonal / text button | `Button.tsx` |
| Toggle button group | `SegmentedButtonGroup.tsx` |
| Elevated / filled / outlined card | `Card.tsx` |
| FAB with expandable menu | `FABMenu.tsx` |
| Bottom navigation | `NavigationBar.tsx` |
| Side navigation | `NavigationRail.tsx` |
| Wavy / circular loading | `LoadingIndicator.tsx` |
| Primary + dropdown button | `SplitButton.tsx` |
| Springy page transitions | Astro `ViewTransitions` + CSS |
| Dark mode toggle | `applyM3Theme(seed, isDark)` |

---

## Troubleshooting

**Q: Colors look inconsistent between components?**
A: Ensure `tokens.css` is imported globally in `Layout.astro`, not scoped to individual components.

**Q: Framer Motion springs feel too bouncy on mobile?**
A: Increase `damping` (try 30–40) and reduce `stiffness` (200–300) for mobile-targeted interactions.

**Q: Astro page transitions jarring?**
A: Use `<ViewTransitions />` and define `::view-transition-old/new` CSS. Ensure elements have unique IDs for shared element transitions.

**Q: Dark mode flickers on load?**
A: Apply `data-theme` attribute in a blocking inline `<script>` (no `type="module"`) in `<head>` before body renders.

**Q: Tailwind M3 classes not working?**
A: Verify `tailwind.config.js` extends theme with CSS variable references and that `tokens.css` is loaded before Tailwind processes the page.

**Q: Color contrast failing with M3 palette?**
A: Only use officially paired M3 on-color tokens (e.g. `on-primary` on `primary`). Never mix roles without checking contrast manually.
