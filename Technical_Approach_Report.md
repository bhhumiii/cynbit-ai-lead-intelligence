# Technical Approach Report
## Cynbit AI Lead Intelligence

## 1. Architecture
CSV upload → schema validation → numeric/type normalization → weighted scoring → priority/action mapping → dashboard charts and filters → CSV export.

## 2. Technology choices
- **Python:** implementation language and data processing.
- **Streamlit:** rapid interactive UI for an assessment prototype.
- **Pandas:** CSV parsing, validation, transformations, aggregation.
- **Plotly:** interactive charts.
- **No external LLM/API:** keeps the demo reproducible, inexpensive, and free of API-key dependencies.

## 3. Data schema
The prototype expects `company`, `source`, `service_interest`, `budget`, `timeline`, `engagement_score`, and `company_size`. The included sample data is synthetic. For a real pilot, define field ownership, allowed values, missing-value policy, consent, access permissions, and retention.

## 4. Scoring logic
A transparent heuristic is used:
- engagement score: 35%;
- normalized budget: 30%;
- timeline urgency: 25%;
- source quality assumption: 10%.

The weighted sum yields a score from 0 to 100, then maps to Low (0–44), Medium (45–69), and High (70–100). These weights are illustrative assumptions, not learned parameters. They should be validated with stakeholders and outcomes.

## 5. Why not train an ML model immediately?
No real labeled CRM dataset was provided. Training a model on invented data and reporting its accuracy would be misleading. If historical outcomes are available, define a target such as qualified opportunity or meeting booked, use time-aware validation, check class imbalance and leakage, and compare against a simple baseline.

## 6. Reliability and error handling
- validates required column names;
- reports missing columns;
- handles empty CSV files;
- converts budget and engagement to numeric values for scoring;
- allows filters and export;
- uses a built-in demo dataset to make the app testable without private data.

## 7. Production architecture (future)
Authenticated CRM connector → consented/minimized data store → validation and feature pipeline → scoring service → CRM task recommendation → monitoring dashboard. Add audit logs, role-based access, rate limits, secure secrets management, and human override.

## 8. Evaluation plan
Offline: compare scoring approaches on a held-out time period; measure precision/recall at top-k and calibration where appropriate.  
Pilot: track response time, meeting-booked rate by priority, override rate, and user feedback.  
Operational: monitor missing fields, score distribution drift, failures, and access logs.

## 9. Deployment
Run locally with `python -m streamlit run app.py`. For sharing, push source and `requirements.txt` to a GitHub repository and deploy via Streamlit Community Cloud. Do not commit confidential customer data or API keys.
