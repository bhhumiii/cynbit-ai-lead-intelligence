# Cynbit AI Lead Intelligence

A Streamlit proof of concept for prioritizing incoming sales leads. It supports CSV upload, transparent heuristic scoring, priority filters, charts, explanations, and CSV export.

## Business opportunity
Cynbit's public website describes AI agents for leads and coordination, LLM automation, and CRM automation. This prototype explores how lead triage could help a sales team prioritize follow-up. It is a proposed opportunity, not a claim that Cynbit currently has this problem or that the company uses this tool.

## Important scope note
The app uses an explainable weighted heuristic, not a trained predictive ML model. It does not claim predictive accuracy. Real deployment would require historical CRM data with outcome labels (for example, meeting booked or opportunity won), stakeholder validation, privacy review, and offline evaluation.

## Run locally
```bash
python -m venv .venv
# Windows PowerShell
.venv\\Scripts\\Activate.ps1
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

## Input CSV schema
Required columns:
- `company`: organization name
- `source`: Website, Referral, LinkedIn, Social Media, or Other
- `service_interest`: requested service
- `budget`: numeric budget in INR
- `timeline`: Within 1 month, Within 3 months, or Exploring
- `engagement_score`: numeric 0–100, for demo purposes
- `company_size`: Small, Medium, or Large

A demo dataset is included at `sample_leads.csv`.

## Scoring design
- Engagement: 35%
- Budget: 30%
- Timeline urgency: 25%
- Lead source: 10%

Scores are grouped into Low (0–44), Medium (45–69), and High (70–100). These weights and thresholds are illustrative and should be calibrated with real business outcomes.

## Deployment
Push this repository to GitHub, then deploy through Streamlit Community Cloud. Set the main file to `app.py` and ensure `requirements.txt` is at the repository root.
