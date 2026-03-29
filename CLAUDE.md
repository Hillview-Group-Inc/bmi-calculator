# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A zero-build BMI calculator SPA. No package manager, no bundler, no build step — open `index.html` directly in a browser.

## Running the App

Open `index.html` directly in a browser. No server or build process required.

For a quick local server if needed:
```bash
python -m http.server 8080
# or
npx serve .
```

## Architecture

Two files only:

- **`index.html`** — loads React 18, Tailwind CSS, Lucide Icons, and Babel Standalone via CDN; mounts `<BMICalculator />` to `#root`
- **`app.js`** — single React functional component (`BMICalculator`) with all logic inline

Dependencies are loaded from CDNs (no `node_modules`). Babel Standalone handles JSX transformation in the browser at runtime.

## Key Implementation Details

**State:** All state lives in `BMICalculator` via `useState`/`useEffect` — unit system toggle, height/weight inputs, BMI result, and history.

**Persistence:** Calculation history is stored in `localStorage` under key `"bmiHistory"` (max 5 entries). Loaded on mount.

**BMI Logic:**
- Imperial path: converts feet+inches → cm, pounds → kg, then applies standard formula
- Metric path: direct calculation from cm/kg inputs
- Categories: Underweight (<18.5), Normal (18.5–24.9), Overweight (25–29.9), Obese (≥30)
