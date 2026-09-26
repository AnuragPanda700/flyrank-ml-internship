# Portfolio Visual Identity Kit & Content Map

**FlyRank AI Internship — General AI Fluency Week 3**  
**Student:** Anurag Panda (`anu-rag-panda`)  
**Milestone:** *Week 3: Map It & Give It a Face (Consistency, Not Talent & Frame, Not Upstage)*  

---

## Overview

This directory contains the complete deliverables for **General AI Fluency Week 3**. The goal of this milestone is to establish a clear, professional visual identity and content architecture for the portfolio, ensuring that **design acts as the frame, not the painting**.

### Core Deliverables in this Package:
1. **Portfolio Content Map & Identity Plan (`portfolio-plan.md`):**
   - **One-Line Claim:** *"I build practical machine learning solutions using real-world datasets and clearly explain the reasoning behind my technical decisions."*
   - **Target Audience:** ML Hiring Managers & Senior Engineers looking for evidence of technical rigor.
   - **Desired Action:** Invite for technical interview.
   - **Voice Card:** `Direct` · `Honest` · `Curious` · `Practical` · `Simple` · `No Buzzwords`.
   - **Information Architecture:** Structured visitor journey from Landing Claim to Featured Proof to Contact.
   - **Identity Kit:** Typography hierarchy (`Inter` + `JetBrains Mono`), 4-color palette, and Claude Project Style Note.
   - **Image Curation ("Kill Your Darlings"):** Comprehensive evaluation comparing real technical proof (`real_capture.png`) against rejected decorative stock art (`rejected_ai_image.png`).

2. **Interactive Identity Showcase (`index.html`):**
   - Single-page, fully responsive visual identity guide.
   - Interactive color swatches with hex codes, typography specimens, SVG logo badge/favicon previews, and a side-by-side "Kill Your Darlings" evaluation.

3. **Production Assets (`assets/`):**
   - `ap-logo.svg`: Vector monogram logo mark.
   - `ap-favicon.svg`: Vector favicon badge.
   - `real_capture.png`: Authentic terminal capture of ML-04 data contract execution, 9.8M rows, and leakage experiment metrics.
   - `rejected_ai_image.png`: Critically evaluated and rejected decorative AI illustration ("AI slop" glowing brain).

---

## Directory Structure

```text
portfolio-identity/
├── README.md                 # This overview guide
├── portfolio-plan.md         # Full markdown specification of identity & content map
├── index.html                # Visual showcase & design system specimen (open in browser)
└── assets/
    ├── ap-logo.svg           # Monogram logo mark (AP)
    ├── ap-favicon.svg        # Scalable vector favicon
    ├── real_capture.png      # Authentic technical capture (Proof / The Painting)
    └── rejected_ai_image.png # Evaluated & rejected AI visual ("Kill Your Darlings")
```

---

## Viewing the Visual Identity Guide

To inspect the live visual identity system:
1. Open `portfolio-identity/index.html` in any modern web browser (Edge, Chrome, Firefox).
   - In PowerShell: `Start-Process "portfolio-identity/index.html"`
2. The page renders the exact design system (Inter typography, color palette, logo assets, and image evaluation side-by-side).

---

## Claude Project Style Note

To maintain visual consistency across all Claude-assisted drafting and portfolio artifacts, copy the following snippet into the Claude Project's Custom Instructions:

```text
Portfolio Visual Identity: Use Inter for headings (SemiBold/Bold) and body text (Regular, 16px/1.6 line height). Use JetBrains Mono for code and metrics. Colors: Canvas #F8FAFC, Cards #FFFFFF with border #E2E8F0, Text #0F172A (muted #64748B), Accent #2563EB. Mood: Clean, technical, restrained, high-contrast. The design must act as a frame that highlights real code and empirical validation without decorative distractions.
```
