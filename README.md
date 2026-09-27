# PROHEALTH CARE LABORATORY — Payment Receipt Generator

A React + Vite + Tailwind CSS single-page app for generating and printing
customer payment receipts.

## Setup

```bash
npm install
npm run dev
```

Then open the URL Vite prints (usually http://localhost:5173).

## Build for production

```bash
npm run build
npm run preview   # to test the production build locally
```

`npm run build` outputs a static site to `dist/` that can be hosted anywhere
(e.g. Netlify, Vercel, an internal server, or opened directly).

## Editing the lab's identity

All fixed laboratory details (name, tagline, email, phone, document title)
live in one place: `src/labConfig.js`. Change them there and every receipt
updates.

## How it works

- **Left column** — the data entry form (`ReceiptForm`, `PatientDetails`,
  `TestList`): patient details, one or more tests/services with price,
  discount, and payment mode.
- **Right column** — a live receipt preview (`ReceiptPreview`,
  `ReceiptHeader`, `ReceiptTable`, `ReceiptSummary`) that updates immediately
  as you type.
- **Print Receipt** button validates the form, then calls `window.print()`.
  CSS in `src/index.css` hides everything except the receipt itself
  (`#receipt-print-area`) during printing and sizes it for A4.

Total, payable amount, and the amount-in-words conversion
(`src/utils/numberToWords.js`, Indian numbering system: Lakh/Crore) are all
calculated automatically — no manual math required. The "Received" field
auto-fills with the payable amount but can be edited manually if a different
amount was actually collected.

## Test scenario (from the original brief)

| Field | Value |
|---|---|
| Patient ID | 108950 |
| Date | 2026-05-18 |
| Name | PAYAL |
| Age / Sex | 29 / Female |
| Ref Dr. | SELF |
| Test 1 | URINE ROUTINE — ₹100 |
| Test 2 | CULTURE AND SENSITIVITY URINE — ₹350 |
| Discount | ₹0 |
| Payment Mode | Cash |

Expected result: **Total ₹450**, **Received ₹450**,
**Amount in Words: Four Hundred Fifty Rupees Only**.
