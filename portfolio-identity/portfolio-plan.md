# Portfolio Visual Identity & Content Map — General AI Fluency Week 3

**Author:** Anurag Panda  
**Program:** FlyRank AI Internship — General AI Fluency Track  
**Milestone:** Week 3: *Map It & Give It a Face (Consistency, Not Talent & Frame, Not Upstage)*  
**Date:** September 2026  

---

## Core Philosophy: "Frame, Not Upstage"

> *"The design is the frame, not the painting. Your work is the painting."*

A portfolio exists to provide tangible evidence of technical competence. For an Applied Machine Learning Engineer, the "painting" consists of rigorous data contracts, signal audits, clean code, leakage-free models, and honest validation metrics. 

If the portfolio's visual design is loud, flashy, or dominated by dramatic AI-generated illustrations, the design upstages the work. Inspired by *Refactoring UI* (Wathan & Schoger), this identity system establishes a restrained, high-contrast, cohesive visual foundation. By making a handful of deliberate typography, color, and spacing decisions once, every future case study inherits a polished, professional look without needing to be reinvented.

---

## 1. The One-Line Claim & Target Strategy

### The One-Line Claim (Value Proposition)
> **"I build practical machine learning solutions using real-world datasets and clearly explain the reasoning behind my technical decisions."**

### Target Audience ("One Person")
- **Target:** Machine Learning Hiring Managers, Technical Recruiters, and Senior ML Engineers evaluating candidates for entry-level Machine Learning Engineer roles and Applied ML internships.
- **Mindset of the Reader:** Busy, skeptical of superficial AI hype, looking for verifiable technical competence, careful communication, and genuine understanding of data reality.

### Desired Action ("One Action")
- **Action:** Invite Anurag Panda for a technical interview to discuss real projects and problem-solving methodology.

### Voice Card
- **Attributes:** `Direct` · `Honest` · `Curious` · `Practical` · `Simple` · `No Buzzwords`
- **Guiding Rule:** State what was observed, measured, and decided. Avoid exaggerated adjectives ("revolutionary", "cutting-edge", "game-changing"). Let the data and code speak.

---

## 2. Content Map & Information Architecture

### Visitor Journey
```text
Landing (Hero Claim) ──► Evidence (Featured Case Studies) ──► Validation (ML Methodology) ──► Action (Contact / Interview)
```

### Site Structure & Page Sections

1. **Header & Navigation:**
   - Minimalist monogram logo (`AP`).
   - Clean text links: `Case Studies`, `About & Foundation`, `GitHub`, `Resume`.
   - Contact CTA button.

2. **Hero Section (First 5 Seconds):**
   - **Headline:** The One-Line Claim in bold, clear typography.
   - **Supporting Subtext:** Computer Science student specializing in applied machine learning, real-world data pipelines, and honest model validation.
   - **Primary Action (CTA):** `[ View Case Studies ]` (anchors directly to evidence).
   - **Secondary Action:** `[ Download Resume ]` / `[ GitHub Profile ]`.

3. **Featured Case Studies (The Proof):**
   - Presented as deep-dive engineering case studies, not a generic card grid.
   - **Case Study 1 (Lead Project):** *FlyRank Search Intelligence Data Contract & Leakage Audit (ML-04)*
     - Problem: Multi-million-row warehouse panel with unbalanced history and high risk of circular feature leakage.
     - Method: DuckDB remote queries over 9.8M March 2026 fact rows, grain verification, availability filtering (`IS TRUE`), deliberate leakage experiment (leaky ROC AUC 0.9445 vs. honest ROC AUC 0.6662).
     - Proof: Real code and terminal output screenshot (`assets/real_capture.png`).
   - **Case Study 2:** *Grid Guardian AI — Predictive Grid Monitoring*
     - Problem: Complex power-grid disturbance detection and localization on real measurement data.
     - Method: Preprocessing, baseline scoring, and honest temporal holdout validation.
   - **Case Study 3:** *Content Refresh Opportunity Scoring*
     - Problem: Prioritizing declining content for SEO interventions.
     - Method: Hand-crafted rule baseline vs. tree-based scoring model.

4. **About & Engineering Foundation:**
   - Short, punchy bio aligned with the Voice Card.
   - Core Technical Stack: Python, DuckDB, Pandas, Scikit-Learn, PyTorch, SQL, Git.
   - The "Before vs. After" mindset shift (moving from prompt-dependent coding to evidence-driven engineering).

5. **Footer & Action:**
   - Direct invitation to connect for technical discussions and interviews.
   - Links: GitHub (`@anu-rag-panda`), LinkedIn, Email.

### Gather List (Still Needed Before Launch)
- [ ] Final ATS-optimized PDF export of updated CV.
- [ ] Recorded animated GIF / walkthrough link for Grid Guardian dashboard.
- [ ] Deployed capstone research paper URL (for submission in `submission/paper_url.txt`).

---

## 3. The Identity Kit (Design System)

### Typography Hierarchy
| Element | Font Family | Weight | Size / Line Height | Purpose |
|---|---|---|---|---|
| **Headings (H1/H2)** | `Inter`, sans-serif | Bold (700) / SemiBold (600) | 32px–40px / 1.2 | Crisp, clean, authoritative modern headings without decorative clutter. |
| **Subheadings (H3)** | `Inter`, sans-serif | Medium (500) | 20px–24px / 1.3 | Structural section dividing headers. |
| **Body Text** | `Inter`, sans-serif | Regular (400) | 16px / 1.6 | High legibility for long-form case studies and technical reasoning. |
| **Code & Metrics** | `JetBrains Mono` / `Roboto Mono` | Regular / Medium | 14px / 1.5 | Fixed-width precision for SQL snippets, schema tables, and ROC-AUC numbers. |

### Color Palette (Four Core Roles)
| Role | Color Name | Hex Code | Visual Swatch & Usage |
|---|---|---|---|
| **Accent / Action** | Royal Blue | `#2563EB` | Primary buttons, active links, key metric highlights. Confident, technical, high-trust. |
| **Text Primary** | Deep Slate | `#0F172A` | Primary text and major headers. High contrast against light background (WCAG AAA). |
| **Text Muted** | Slate Gray | `#64748B` | Secondary text, timestamps, captions, table headers. |
| **Surface (Card)** | Pure White | `#FFFFFF` | Background for case study cards, code boxes, and interactive elements. |
| **Canvas Background** | Soft Slate | `#F8FAFC` | Main page canvas; softens contrast compared to harsh pure white. |
| **Border / Divider** | Light Slate | `#E2E8F0` | Subtle hairline borders defining structure without visual heavy-lifting. |

### Monogram Logo & Favicon
- **Concept:** A clean, geometric rounded square with gradient accent containing the bold monogram initials `AP` (Anurag Panda).
- **Files:**
  - Full Logo: `assets/ap-logo.svg`
  - Favicon: `assets/ap-favicon.svg`

### Style Note (For Claude Project Custom Instructions)
```text
Portfolio Visual Identity: Use Inter for headings (SemiBold/Bold) and body text (Regular, 16px/1.6 line height). Use JetBrains Mono for code and metrics. Colors: Canvas #F8FAFC, Cards #FFFFFF with border #E2E8F0, Text #0F172A (muted #64748B), Accent #2563EB. Mood: Clean, technical, restrained, high-contrast. The design must act as a frame that highlights real code and empirical validation without decorative distractions.
```

---

## 4. Image Curation: "Kill Your Darlings" (Real Capture vs. Rejected AI Image)

A key lesson of Week 3 is critically evaluating visual assets rather than adopting them merely because AI generated something flashy.

### Comparison Table

| Dimension | The Real Capture (Chosen) | The AI Image (Rejected) |
|---|---|---|
| **Visual Asset** | `assets/real_capture.png` | `assets/rejected_ai_image.png` |
| **Subject** | Real syntax-highlighted terminal capture of FlyRank ML-04 data contract execution, 9.8M warehouse row count, and deliberate leakage experiment scores. | A glowing 3D holographic digital brain with neon circuitry, lens flares, and floating buzzwords ("DATA PROCESS", "FUTURE TECH"). |
| **Role in Portfolio** | **The Painting:** Direct, undeniable proof of technical capability and disciplined machine learning validation. | **Distracting Decoration:** Flashy visual noise that upstages and obscures the actual work. |
| **Recruiter Perception** | *"This candidate actually executes queries on big data warehouses, understands leakage, and reports honest metrics."* | *"This candidate used Midjourney/DALL-E to generate generic stock art to mask a lack of real projects."* |
| **Informational Value** | High: Shows actual numbers, ROC-AUC deltas ($\Delta = -0.2783$), and SQL queries. | Zero: Conveys no technical information about models, algorithms, or datasets. |
| **Alignment with Voice Card** | Perfect fit: Direct, Honest, Practical, Simple. | Complete mismatch: Cluttered, hype-driven, buzzword-heavy. |
| **Final Decision** | **KEPT (Featured in Lead Case Study)** | **REJECTED ("Killed as a Darling")** |

### Detailed Evaluation of the Rejected AI Visual
The AI-generated image (`assets/rejected_ai_image.png`) was intentionally prompted to see if a visual could symbolize "artificial intelligence". While visually striking at first glance, critical evaluation revealed:
1. **It Upstages the Work:** The high-saturation blue and violet neon immediately draws the viewer's eye away from the case study headline and technical metrics.
2. **It is "AI Slop":** It uses cliché tropes (glowing brain, circuit boards, glossy glass) that hiring managers see on thousands of generic tech sites.
3. **It Violates the Core Premise:** The assignment emphasizes that proof comes first, decoration second. A decorative brain proves nothing about machine learning skill; a terminal output showing `roc_auc_score` on an honest test set proves genuine skill.
