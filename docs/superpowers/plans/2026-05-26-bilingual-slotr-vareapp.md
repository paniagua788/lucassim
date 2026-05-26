# Bilingual Slotr & VareApp Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add Spanish/English bilingual support to the Slotr and VareApp landing pages using the same client-side DOM toggle pattern as the portfolio page.

**Architecture:** Extend the shared `Navbar.astro` component with an optional `showLangToggle` prop. Duplicate all page content (frontmatter constants and markup) for English inside `slotr.astro` and `vareapp.astro`, wrapping each language in `data-lang` containers. Include the exact toggle script from `portfolio.astro` at the bottom of each page.

**Tech Stack:** Astro 6, TypeScript, Tailwind CSS 4, static HTML

---

## Files Modified

| File | Change |
|---|---|
| `src/components/Navbar.astro` | Add optional `showLangToggle` prop and render ES/EN toggle buttons |
| `src/pages/slotr.astro` | Duplicate constants and all markup for English; add toggle script |
| `src/pages/vareapp.astro` | Duplicate constants and all markup for English; add toggle script |

---

## Commits

- `4f46c34` — feat: add optional language toggle to Navbar
- `3aba46a` — feat(slotr): add English page content and language toggle
- `0eac2c0` — feat(vareapp): add English page content and language toggle

---

## Implementation Summary

### Task 1: Navbar toggle ✅
Added `showLangToggle?: boolean` prop to `Navbar.astro`. When true, renders ES/EN buttons styled identically to portfolio toggle (`bg-surface rounded-lg`, `bg-white text-gray-900` for active, `text-muted` for inactive).

### Task 2-3: Slotr bilingual ✅
- Added `featureCategoriesEn`, `targetEn`, `pricingRangesEn` constants
- Wrapped all page content in `<div data-lang="es">` and `<div data-lang="en" class="hidden">`
- Added toggle script (identical to portfolio.astro)
- Changed `<Navbar />` to `<Navbar showLangToggle={true} />`

### Task 4-5: VareApp bilingual ✅
- Added `featureCategoriesEn`, `targetEn`, `esencialIncludedEn`, `esencialExcludedEn`, `proIncludedEn` constants
- Wrapped all page content in `<div data-lang="es">` and `<div data-lang="en" class="hidden">`
- Added toggle script (identical to portfolio.astro)
- Changed `<Navbar />` to `<Navbar showLangToggle={true} />`

### Task 6: Build verification ✅
- `npm run build` passes without errors
- All 4 pages generated: `/`, `/portfolio`, `/slotr`, `/vareapp`

---

## Key Design Decisions

1. **Pattern matches portfolio**: `data-lang` containers + IIFE toggle script + Spanish default
2. **No persistence**: Language state not stored in localStorage or URL — resets to Spanish on reload (same as portfolio)
3. **No `<html lang>` change**: Portfolio doesn't update it dynamically either — consistency
4. **No third language consideration**: Not in scope per spec

---

## Testing Checklist

- [x] Build passes without errors
- [ ] Toggle ES/EN works on `/slotr`
- [ ] Toggle ES/EN works on `/vareapp`
- [ ] Toggle visual matches portfolio toggle
- [ ] Home page navbar does NOT show toggle
- [ ] Animations work in both languages
- [ ] Bento grid renders correctly in both languages