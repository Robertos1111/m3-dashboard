# GlobalCore M3 — Mirror/Wet Coater Readiness Dashboard

Single-file interactive dashboard for tracking QC test readiness across 4 mirror/wet-coater plants (GulfGuard KSA, Nongkhae TH, El Marqués MX, Tatui BR). Built for Global Quality SME sharing via GitHub Pages.

**Version:** 2.4 · **Updated:** 2026-04-14

---

## Live URL

Once deployed to GitHub Pages: `https://<your-username>.github.io/m3-dashboard/`

## What's in this folder

```
m3-dashboard/
├── index.html                      ← the dashboard (open this in a browser)
├── Plant_Input_GulfGuard.xlsx      ← source Raw Materials file from Ali Alahmed
├── README.md                       ← this file
└── GITHUB_SETUP.md                 ← 5-minute deploy guide
```

The dashboard is **a single HTML file** with all libraries loaded from public CDNs (React, Babel, SheetJS/XLSX). No build step, no npm, no server. Opens directly in any modern browser.

---

## How sharing edits works (no backend required)

GitHub Pages serves static files — it can't save your edits back to the server. Use the built-in **Share & Sync** feature instead:

1. Open the dashboard, make your edits on the **M3 QI Config** tab
2. Scroll to **Configuration Summary → Share & Sync**
3. Click **⬇ Export Full State (JSON)** → a file downloads
4. Send that file to a colleague (email, Slack, Teams, Box, SharePoint...)
5. Recipient opens the dashboard URL and clicks **⬆ Import Full State (JSON)** → selects the file → sees all your edits

No tokens, no APIs, no data leaves the browser unless you explicitly download a file.

---

## Feature summary (v2.4)

### Dashboard tabs
- **Overview** — plant status cards, coverage stats
- **QC Heatmap** — visual matrix of which tests each plant performs
- **Frequency Detail** — test-by-test frequency breakdown
- **Gap Analysis** — identify tests not being done at each plant
- **M3 Paths** — integration strategy visualization
- **M3 QI Config** — heart of the tool: configure WCO tests per plant, Path A (GPIS → WCO001 PASS/FAIL) or Path B (full WCO001–WCO019 with parameters)
- **RM QI Config** — define Raw Material QI tests from scratch
- **Raw Materials** — consolidated 4-plant raw material matrix

### What's new in v2.4
- GulfGuard (KSA) raw materials data pre-loaded from Ali Alahmed's submission → **3/4 plants received**
- Path B QI Config: editable Description, Type dropdown (Qualitative / Quantitative / Numeric)
- Numeric fields (Max/Min/Target/Decimals/UoM) auto-disable when Type = Qualitative
- Delete button per row; Reset Plant Config to restore defaults
- Add Custom Test now works with partial data (auto-generates CUSTOM_NNN code)
- QC Matrix Map column removed
- Multi-sheet professional Excel export (6 sheets)
- Full State Export/Import to share edits with colleagues

---

## Contact

**Robert Skowron** — Global Quality SME (rskowroncorpo@gmail.com)
