# Procurement Dashboard Repository Package

This package is designed to make the Power BI project easy for a recruiter, hiring manager, or technical reviewer to understand within a few minutes.

```text
repo_package/
│
├── Procurement.pbix
├── README_procurement.md
├── Procurement_Case_Study.md
├── procurement-repo-structure.md
│
├── docs/
│   ├── procurement-data-dictionary.md
│   ├── procurement-dax-reference.md
│   └── assets/
│       ├── executive-overview.png
│       ├── operational-performance.png
│       ├── risk-radar.png
│       ├── wireframe-executive.png
│       ├── wireframe-performance.png
│       └── wireframe-risk-radar.png
│
└── screenshots/
    ├── executive-overview.png
    ├── operational-performance.png
    └── risk-radar.png
```

## Recommended GitHub presentation order

### README.md
The README should be the recruiter entry point. It should answer:

- what the project is
- what business problem it solves
- what Power BI skills are demonstrated
- what the three report pages do
- what the major KPIs mean
- what makes the project technically interesting
- how the dashboard was designed
- how to review the `.pbix`

### screenshots/
These should contain the finished report images so a recruiter can understand the result without downloading Power BI.

### docs/
These should contain the deeper technical evidence for reviewers who want to inspect the work beyond the dashboard screenshots.

### Procurement.pbix
The working Power BI file should remain the main technical artifact.

## Recruiter-first hierarchy

**README → screenshots → case study → technical documentation → PBIX**

That order keeps the portfolio accessible to both nontechnical hiring managers and technical BI reviewers.
