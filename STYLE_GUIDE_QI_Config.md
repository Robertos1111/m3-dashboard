# M3 QI Config — Excel Export Style Guide

**Reference file:** `M3_QI_Config_ELM_2026-04-14.xlsx` (El Marqués, Path B, v2.4)
**Purpose:** Every Excel report generated from the M3 Readiness Dashboard MUST match this style exactly — regardless of plant (GulfGuard, Nongkhae, El Marqués, Tatui) or path (A/B).

---

## Global rules

- **Font:** Calibri throughout
- **Row 1 height:** 28 px; Row 2 height: 20 px; Row 3 (header) height: 22 px; data rows: 18 px
- **No freeze panes** (per reference — optional: freeze row 3 for long sheets)
- **No charts, no pivots, no conditional formatting rules** (colors are baked into cell fill)
- **Sheets (in order):** `Summary` → `QI Config Path A` OR `QI Config Path B` (depending on plant path) → `QC Tests` → `Raw Materials`

---

## Color palette (ARGB hex — include `FF` alpha prefix in openpyxl / SheetJS style)

| Token | Hex | Use |
|---|---|---|
| `NAVY` | `FF1F4E79` | Row 1 title bar (white bold text, 16pt) |
| `BLUE_MID` | `FF2E75B6` | Row 2 subtitle bar (white bold text, 11pt) |
| `SLATE_BG` | `FFF1F5F9` | Header-row cells and key-label cells (dark navy bold text) |
| `WHITE` | `FFFFFFFF` | Odd data rows |
| `GRAY_ZEBRA` | `FFFAFBFC` | Even data rows (zebra striping) |
| `GREEN_BG` | `FFDCFCE7` | "Yes" / "Performed" / "PASS" pills |
| `GREEN_TEXT` | `FF16A34A` | Text on green pills |
| `GREEN_TEXT_DARK` | `FF166534` | "Quantitative" label text |
| `INDIGO_BG` | `FFE0E7FF` | "Qualitative" label background |
| `INDIGO_TEXT` | `FF3730A3` | "Qualitative" label text |
| `NAVY_TEXT` | `FF1F4E79` | Header row text, WCO code text |
| `GRAY_LABEL` | `FF374151` | Summary key-label text |
| `GRAY_DASH` | `FF94A3B8` | Em-dash `—` placeholder text |
| `TEXT_BODY` | `FF111827` | Default body text |

---

## Row 1 — Title bar (all sheets)

- **Merged:** `A1:<lastCol>1`
- **Fill:** `NAVY`
- **Font:** Calibri 16pt, bold, color `WHITE`
- **Align:** horizontal=left, vertical=center, indent=1
- **Value format:** `"<Section Name> — <Plant> (<CountryCode>)"` (e.g., `Path B — Full M3 QI Request (El Marqués (MX))`)
- For `Summary` sheet specifically: `"GlobalCore M3 — Mirror / Wet Coater Readiness"`

## Row 2 — Subtitle bar (all sheets)

- **Merged:** `A2:<lastCol>2`
- **Fill:** `BLUE_MID`
- **Font:** Calibri 11pt, bold, color `WHITE`
- **Align:** left, vertical=center, indent=1
- **Value:** sheet-specific context (see per-sheet section below)

## Row 3 — Column headers

- **Fill:** `SLATE_BG`
- **Font:** Calibri 11pt, bold, color `NAVY_TEXT`
- **Align:** center for short/numeric cols, left for long text cols
- **Border:** thin bottom border (`FFCBD5E1`)

## Data rows (from row 4)

- **Zebra:** odd row index → `WHITE`; even → `GRAY_ZEBRA`
- **Font:** Calibri 10pt, color `TEXT_BODY`
- **Align:** `#` column → center; text cols → left; numeric cols → right; status/pill cols → center
- **Em-dash placeholder:** when value is missing/N-A, use the character `—` (U+2014), colored `GRAY_DASH`, NOT the escape `\u2014`

### Pill cells (conditional coloring)

| Value | Fill | Text color | Bold |
|---|---|---|---|
| `Yes` / `Performed` / `PASS` | `GREEN_BG` | `GREEN_TEXT` | yes |
| `No` / `Not Performed` / `FAIL` | `FFFEE2E2` | `FFDC2626` | yes |
| `N/A` / `TBD` | (inherit zebra) | `GRAY_DASH` | no |
| `Qualitative` | `INDIGO_BG` | `INDIGO_TEXT` | yes, 9pt |
| `Quantitative` | `GREEN_BG` | `GREEN_TEXT_DARK` | yes, 9pt |
| `Numeric` | `FFFEF3C7` | `FF92400E` | yes, 9pt |

---

## Per-sheet specs

### 1. `Summary` — 4 cols (A–D), widths: 28.8 / 40.8 / 20.8 / 26.8

Row 2 subtitle: `"QI Configuration Export  ·  <Plant> (<CC>)  ·  <YYYY-MM-DD>"`

Row 3 merged A3:D3 fill `SLATE_BG` — section header `"Plant Information"` (12pt bold, `NAVY_TEXT`)

Rows 4–8: two-column key/value pairs (A=label1, B=value1, C=label2, D=value2)
- Labels fill `SLATE_BG`, bold, `GRAY_LABEL`
- Values no fill, regular, `TEXT_BODY`

Standard keys: `Plant | Region`, `Plant ID | Status`, `System | GPIS Used`, `Integration Path | QI Request Freq.`, `Data Owner | Dashboard Ver.`

Row 11 merged A11:D11 fill `SLATE_BG` — next section header (e.g., `"Report Contents"`)
Row 16 merged A16:D16 — footer with generation timestamp (11pt regular, `GRAY_LABEL`)

### 2. `QI Config Path A` / `QI Config Path B` — 12 cols (A–L)

Widths: 5.8 / 14.8 / 40.8 / 15.8 / 10.8 / 12.8 / 12.8 / 12.8 / 8.8 / 10.8 / 12.8 / 14.8
Row 2: `"QI Request Frequency: <freq>"`
Headers: `# | WCO Code | Description | Type | Enabled | Max | Min | Target | Dec | UoM | Result | Source`

- `WCO Code` col: bold `NAVY_TEXT`
- `Type` col: pill (Qualitative/Quantitative/Numeric)
- `Enabled` col: pill (Yes/No)
- `Max/Min/Target`: right-aligned numeric; `—` when not applicable (Qualitative rows)
- `Result` col: pill (PASS/FAIL) or `—`

### 3. `QC Tests` — 9 cols (A–I)

Widths: 5.8 / 36.8 / 32.8 / 14.8 / 14.8 / 22.8 / 22.8 / 12.8 / 14.8
Row 2: `"<N> performed  ·  <M> not performed"`
Headers: `# | QC Test | Purpose | Test Type | Status | Frequency | Tool | Mode | Recorded In`

- `Status` col: pill (Performed=green, Not Performed=red, N/A=gray)

### 4. `Raw Materials` — 9 cols (A–I)

Widths: 5.8 / 28.8 / 32.8 / 14.8 / 16.8 / 14.8 / 14.8 / 12.8 / 40.8
Row 2: `"Awaiting plant response"` OR `"<N> of <M> materials confirmed"`
Headers: `# | Material Category | Typical Examples | Used on Line? | Quality Critical? | Visible in M3? | Lot-Controlled? | Risk Level | Comments`

- `Risk Level` col: pill (High=red, Medium=amber, Low=green)

---

## SheetJS / ExcelJS implementation notes

- SheetJS community edition does NOT support cell styling. Use **ExcelJS** (`exceljs` npm) or **SheetJS Pro**.
- Recommendation: switch the dashboard export from `xlsx` (SheetJS community) to `exceljs`. API is cleaner for styling.
- Alternative: keep SheetJS for value writing, post-process with `xlsx-js-style` fork (drop-in replacement that supports styles).

### Canonical cell-writing helper (pseudocode)

```js
function titleRow(ws, sheet, plantLabel) {
  ws.mergeCells('A1:L1');
  const c = ws.getCell('A1');
  c.value = `${sheet} — ${plantLabel}`;
  c.fill = { type:'pattern', pattern:'solid', fgColor:{argb:'FF1F4E79'} };
  c.font = { name:'Calibri', size:16, bold:true, color:{argb:'FFFFFFFF'} };
  c.alignment = { horizontal:'left', vertical:'center', indent:1 };
  ws.getRow(1).height = 28;
}
```

Apply the same pattern for subtitle, headers, data rows, and pill cells.

---

## Quality checklist (before any export ships)

- [ ] Calibri everywhere, no Arial/Times
- [ ] Title bar navy, subtitle mid-blue, both white bold
- [ ] Zebra stripes correct (even rows `FAFBFC`, odd `FFFFFF`)
- [ ] Pills use correct fill + text color combo
- [ ] All placeholder dashes are `—` (U+2014) with `GRAY_DASH` color — never the text `\u2014`
- [ ] UTF-8: plant names render (`El Marqués`, not `El Marqu\u00e9s`)
- [ ] Column widths match spec per sheet
- [ ] No `#REF!`, `#VALUE!`, `#DIV/0!` errors
- [ ] Merged cells on rows 1 + 2 + sheet-specific section headers only
- [ ] File opens cleanly in Excel 2016+, LibreOffice, and Google Sheets
