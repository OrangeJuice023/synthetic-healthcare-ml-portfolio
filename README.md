# Synthetic Healthcare Data Science Portfolio

End-to-end machine learning portfolio built on a **fully synthetic** healthcare dataset — nine projects across thirteen simulated diagnostic-lab clients. Every patient, result, and figure is fabricated by a generator designed to mirror the structure of real lab data.

**The data is synthetic. The methods are real.**

> ⚗️ **Why synthetic?** Real diagnostic-lab data is confidential and can't be published. So this portfolio runs on a self-authored generator that produces realistic-but-fake data with deliberate, learnable signal in it. The pipelines, feature engineering, and validation are exactly what the same work on real data would require — but nothing here traces back to a real person or organization, which is what makes it safe to publish. The reported metrics demonstrate that the *methods* work; they are not real-world clinical findings.

🔗 **Live site:** _add your Vercel URL here_

---

## The projects

All nine run on the same synthetic 6-table schema. Metrics below come from running real models on the generated data.

| # | Project | Type | Headline result |
|---|---------|------|-----------------|
| 01 | Abnormal Lab Result Predictor | Classification | 0.78 AUC predicting abnormal results from age + test type |
| 02 | Turnaround Time Predictor | Regression | 0.79 R², ~27 min MAE; Monday-morning bottleneck surfaced |
| 03 | Patient Segmentation | Clustering | 5 behavioral segments (K-Means, silhouette 0.36) |
| 04 | Test Bundle Analysis | Association rules | 51% of orders bundled; renal & thyroid panels lift > 6 |
| 05 | Revenue & Discount Anomaly Detection | Anomaly detection | 2.5% flagged via Isolation Forest + Z-score agreement |
| 06 | Support Ticket Intelligence | NLP classification | 0.98 F1 across 5 ticket categories (TF-IDF + LogReg) |
| 07 | SOAP Notes NLP | Topic modeling | 5 clinical topics + severity from free-text notes |
| 08 | Radiology Impression Parser | Multilingual NLP | Organ-level parsing of Bahasa Indonesia impressions, 61% normal |
| 09 | Cross-Client Benchmarking | Comparative analytics | KPI comparison across all 13 synthetic clients |

---

## The data

A single self-contained Python script generates everything. It reads no external data at runtime — distribution shapes (age curves, test mixes, reference ranges, turnaround spreads) are baked in as fixed parameters, and each project has a deliberate, recoverable signal engineered into it.

Six tables per client, shaped like a real lab information system export:

- `patients` — demographics
- `orders` — transactions, discounts, cancellations
- `order_items` — line-level services per order
- `patient_services` — service execution with collection/lock timestamps
- `patient_service_results` — values, reference ranges, and free-text impressions
- plus `support_tickets` (one client) and `soap_analytics` (one client)

A fraction of patient names and addresses are playful pop-culture / fantasy easter eggs — a deliberate signal that no row is a real person.

### Generate it yourself

```bash
pip install pandas numpy openpyxl faker
python generate_synthetic.py ./synthetic-data
# optional: --clients 13 --seed 42
```

This reproduces the same thirteen clients. Change the seed for a fresh dataset.

---

## Tech stack

**Site:** Next.js (App Router) · TypeScript · Tailwind CSS · Recharts · Framer Motion
**Data & ML:** Python · pandas · NumPy · scikit-learn · mlxtend · Faker

## Running the site locally

```bash
pnpm install
pnpm dev
# open http://localhost:3000
```

---

## Project structure

```
.
├── generate_synthetic.py          # the data generator (single source of the dataset)
└── src/
    ├── app/                       # routes: home, projects, methodology, instructions
    ├── components/                # SyntheticBadge, charts, layout, project template
    ├── content/                   # projects.ts + project-details.ts (all 9 projects)
    └── lib/                       # types, helpers
```

---

## A note on honesty

This project exists partly to demonstrate the difference between *synthetic* and *real* — and to show that work can be done cleanly without exposing confidential data. Throughout the site, the data and every metric are clearly labeled synthetic. They are illustrative of method, not real clinical or business outcomes. Please don't cite the numbers here as real-world findings.

## License

MIT — see [LICENSE](LICENSE).

---

_This is a personal portfolio / educational project. It is not an official product of any company, and uses no real patient, physician, or client data._
