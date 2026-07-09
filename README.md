# 📖 Advanced SIP Calculator — The Passbook

> A bank-passbook-styled SIP calculator that goes beyond the standard maturity-value formula — built with Step-Up SIPs, a Goal Planner, inflation adjustment, expense ratio drag, and post-tax return modelling.

**🔗 Live App:** [cpravin2110.github.io/Advanced-SIP-Calculator](https://cpravin2110.github.io/Advanced-SIP-Calculator/)

---

## 🧾 What is this?

Most online SIP calculators only answer one question: *"If I invest ₹X every month at Y% return for Z years, what do I get?"*

This calculator answers the more realistic version of that question — the one a real Indian investor actually cares about:

- What if my SIP amount **increases every year** (step-up), like most salaried investors do?
- How much do I need to invest monthly to hit a **specific goal**, like ₹1 Cr?
- What is that maturity amount actually worth after **inflation** eats into it?
- How much does the **fund's expense ratio** silently shave off my returns?
- What do I actually take home after **capital gains tax**?

The UI is themed as a bank passbook / deposit slip — you "fill a deposit slip" with your investment details, and the app returns a "passbook" showing your ledger, year by year.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Three calculation modes** | SIP Growth, Step-Up SIP, and Goal Planner (reverse-calculates the SIP needed to hit a target corpus) |
| **Step-Up SIP** | Models an annual percentage increase in your monthly instalment, matching how most people actually raise their SIP with salary hikes |
| **Goal Planner** | Set a target corpus (e.g. ₹1,00,00,000) and get the required monthly instalment |
| **One-time lump sum** | Add an optional lump-sum investment on top of the recurring SIP |
| **SIP frequency toggle** | Monthly or Quarterly instalments |
| **Inflation adjustment** | Shows the real, present-day value of your maturity corpus after a configurable inflation rate |
| **Expense ratio drag** | Deducts the fund's annual expense ratio from the gross return before compounding |
| **Tax on gains** | Simplified LTCG modelling — Equity (with the ₹1.25L exemption slab) or Debt/Other (flat slab rate) — to estimate post-tax, in-hand value |
| **Year-wise ledger** | A full year-by-year breakdown: instalment that year, cumulative invested, value at year-end, and gain so far |
| **Passbook UI** | Deposit-slip and bank-ledger visual theme instead of a generic form/dashboard look |

---

## 🧮 How the numbers are calculated

### 1. Regular SIP (future value of a growing annuity)

For a fixed monthly instalment `P`, monthly rate `i = r/12` (where `r` is the annual return), and `n` total months:

```
FV = P × [((1 + i)^n − 1) / i] × (1 + i)
```

The `(1 + i)` at the end accounts for instalments paid at the start of the month (annuity-due), which matches how SIPs are actually debited.

### 2. Step-Up SIP

Instead of a flat `P` every month, the instalment increases by the step-up % at the start of each year. The calculator compounds each year's instalments separately using the formula above, then carries forward the accumulated corpus into the next year at the growth rate, compounding on top of it — repeated for every year of the tenure.

### 3. Goal Planner

Runs the Step-Up SIP / Regular SIP formula in reverse: given a target corpus, tenure, return rate, and step-up %, it solves for the monthly instalment `P` needed to reach that target (via algebraic rearrangement of the FV formula).

### 4. Expense ratio

The fund's annual expense ratio is subtracted from the expected annual return **before** the compounding calculation runs, e.g. a 12% expected return with a 1% expense ratio compounds at an effective 11%.

### 5. Inflation adjustment (real value)

The nominal maturity value is discounted back to today's rupees using the standard real-value formula:

```
Real Value = Maturity Value / (1 + inflation rate)^tenure in years
```

### 6. Tax on gains

- **Equity funds (LTCG):** Gains above ₹1,25,000 are taxed at the applicable LTCG rate; gains up to the exemption threshold are tax-free.
- **Debt / Other:** Gains are taxed at the user-entered slab rate, with no exemption.

> ⚠️ Tax rules are simplified for planning purposes only and should not be relied on for actual tax filing — always confirm current rules with a tax advisor.

### 7. Year-wise ledger

For every year in the tenure, the app logs: that year's total instalments, cumulative amount invested to date, the portfolio's value at year-end (compounded), and the running gain (value − invested).

---

## 🛠️ Tech Stack

- **HTML5** — single-file structure
- **CSS3** — custom passbook/deposit-slip visual theme, no external UI framework
- **Vanilla JavaScript** — all SIP/Step-Up/Goal/tax/inflation math is computed client-side, no backend or API calls
- **GitHub Pages** — static hosting / deployment

No build step, no dependencies — the entire app is a single self-contained HTML file that runs directly in the browser.

---

## 🚀 Running it locally

Since it's a single static HTML file, no installation is required:

```bash
git clone https://github.com/cpravin2110/Advanced-SIP-Calculator.git
cd Advanced-SIP-Calculator
open index.html   # or just double-click the file
```

Or serve it locally with any static server, e.g.:

```bash
python -m http.server 8000
```

---

## 📂 Project Structure

```
Advanced-SIP-Calculator/
├── index.html      # Markup, styling, and calculator logic
└── README.md        # This file
```

*(Update this section if the project is later split into separate CSS/JS files.)*

---

## 📌 Disclaimer

Figures shown are illustrative projections based on the return rate entered by the user. Actual mutual fund returns are market-linked and not guaranteed. Tax and inflation treatment are simplified for planning purposes only — always confirm current rules with a qualified financial or tax advisor before making investment decisions.

---

## 👤 Author

Built by **Pravin** — [GitHub](https://github.com/cpravin2110)

## 📄 License

© 2026 Pravin. All rights reserved.
