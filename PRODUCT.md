# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

- **Primary (published version):** general public in Spanish who are curious about exoplanets and have no training in astronomy. They arrive on their own, often on a phone, and want to understand what has been discovered and how our world compares.
- **Class demo:** the Visual Analytics professor and classmates, watching on a projected desktop screen while the author drives. They judge the clarity of the analysis and the visual encoding.
- Copy is written for the general public. Every technical term (R⊕, M⊕, insolation, transit method, parsec, light-year) gets a short plain-Spanish explanation, which the class audience can also follow.

## Product Purpose

Pizza Planet is a visual explorer of the confirmed exoplanets in the NASA Exoplanet Archive. The walkthrough has five steps: **understand → explore → compare → travel in time → go deeper**. Success means a visitor can find a planet, see where it sits in space, compare its size with Earth's, see when it was discovered, and read its data sheet without misreading missing data.

## Positioning

The explorer runs on a real, dated snapshot of the NASA catalogs (exported 2026-11-12), not on curated examples. Every number on screen traces back to a CSV column. Missing measurements are shown as missing, and derived labels such as "habitable" are marked as approximations.

## Operating Context

- Two delivery contexts, one codebase: (1) a live class demo on a desktop or projector; (2) a published public page used mostly on mobile.
- Served over HTTP (`python -m http.server 8000` locally). `fetch()` reads the CSVs, so `file://` does not work.
- CDN dependencies (Tailwind, three.js r128 + OrbitControls, Font Awesome, Google Fonts) need an internet connection.

## Capabilities and Constraints

- **Single file:** all code stays in one `index.html` on the current stack: Tailwind CDN, three.js r128, Font Awesome. No build step and no framework.
- **Data:**
  - `PSCompPars` (`data/PSCompPars_2026.11.12_16.30.57.csv`, 6,470 planets, 4,862 systems, 84 columns): one row per planet. It is the catalog for the map, search, comparison, timeline and data sheet.
  - `PS` (`data/PS_2026.11.12_16.32.23.csv`, 40,414 rows, ~38 MB): solutions/publications per planet, joined by `pl_name`. Rows are never counted as planets. `default_flag = 1` marks the default solution.
- **Missing values** are shown as "sin dato" and are never treated as 0.
- **Habitability (derived, labeled as an approximation):**
  - "Zona habitable" = `pl_insol` between 0.25 and 1.5 S⊕.
  - "Terrestre" = `pl_rade` ≤ 1.6 R⊕.
  - A planet missing the needed field is "sin dato" for that criterion, not "no".
  - Snapshot counts: 293 planets in the zone, 1,215 terrestrial, 32 meeting both. 541 planets lie within 100 light-years.
- **Provenance:** `pl_bmassprov = "M-R relationship"` means the mass was calculated from the radius (3,034 planets) rather than measured. The data sheet must make the difference between observed, calculated and unknown visible.
- **Must keep:**
  - CSV loading
  - the 3D map, built from RA/Dec/distance and showing the full catalog by default
  - search by planet or system
  - the discovery-method filter
  - the planet data sheet
- **Ranges:** discovery years run from 1992 to 2026. There are 11 discovery methods, dominated by Transit (4,799) and Radial Velocity (1,205). 6,442 planets have a 3D position.

## Brand Commitments

- **Name:** Pizza Planet. Its own identity: no Toy Story logo, rocket or characters.
- **Visual direction:** "Cyber Diner", defined in `design/marca-cyber-diner.md`. It is binding as a style reference.
- **Structure:** binding wireframe of five screens in `design/boceto.png` and `design/boceto-01…05-*.png`.
- **Language:** Spanish.

## Evidence on Hand

- Real data: the two NASA CSVs listed above, with column descriptions in their `# COLUMN` headers.
- Wireframes: `design/boceto*.png`.
- Brand study: `design/marca-cyber-diner.md`.
- No testimonials, partners or external endorsements exist. None should be invented, and the page must not imply NASA endorses it beyond citing it as the data source.

## Product Principles

1. **Data first:** every visual element encodes a real field or is clearly decorative.
2. **Honest gaps:** "sin dato" and "aproximación" are visible states, not hidden defaults.
3. **Explain once, briefly:** the general public gets a one-line meaning for each term at the point of use.
4. **Same truth on every screen:** a planet selected on one screen is the same planet on the next, carried through the walkthrough.
5. **Demo-proof:** it works on a projector at a distance and on a phone in one hand.

## Accessibility & Inclusion

- Respect `prefers-reduced-motion`.
- Do not encode categories by color alone: discovery method also uses shape or a label.
- Text contrast follows the measured ratios in the brand doc. Ultraviolet is never used for text on dark.
- Controls are keyboard-reachable.
- The 3D map has a non-WebGL fallback, so the data stays reachable without it.
