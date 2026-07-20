[README.md](https://github.com/user-attachments/files/30204539/README.md)
# Micah Luftig

### Data Scientist | Licensed Veterinary Technician | MS

I am an LVT with 15+ years of experience primarily in emergency/critical care medicine, and I fell in love with exploring data while working on my
graduate degree which focused heavily on biometry.

**Connect with me:** [LinkedIn](https://www.linkedin.com/in/micah-luftig/) | <m.luftig24@gmail.com>

---

## Projects

### 1. [Animal Shelter Recidivism Prediction](https://github.com/MLuftig/animal-shelter-recidivism-prediction)

- **Problem:** Identifying key risk variables that cause adopted pets to be rapidly returned to local shelter facilities within a 30-day window.
- **Solution:** Developed an end-to-end Python pipeline utilizing SQL joining for feature engineering and a Random Forest classification model, including a documented correction of an early target-leakage issue in the model's training data.
- **Impact:** Found that an animal's age and species are the strongest predictors of return risk — not length of stay, which an earlier version of the model had mistakenly identified as dominant. Dogs return at roughly 2.7x the rate of cats, and the corrected model achieves 76% recall on true return cases.
- **Tech Stack:** `Python`, `SQL`, `Scikit-Learn`, `Pandas`, `Matplotlib`, `Seaborn`

### 2. [Environmental and Lunar Influences on Shelter Volume](https://github.com/MLuftig/moon-phase-weather-shelter-analysis)

- **Problem:** Myth-busting the long-held veterinary belief that lunar cycles impact patient surge volumes, while isolating real weather triggers for both intake volume and shelter mortality.
- **Solution:** Built a multi-layer SQL data engineering extraction pipeline in Python to merge historical shelter data with localized climatology logs, using non-parametric hypothesis testing followed by multivariate regression to properly isolate independent weather effects.
- **Impact:** Debunked the "Full Moon Effect" via robust non-parametric Kruskal-Wallis testing. A follow-up multivariate analysis found that "feels-like" temperature — not barometric pressure — is the primary independent driver of both intake volume and mortality; pressure's apparent effect in isolation was largely a statistical proxy for temperature.
- **Tech Stack:** `Python`, `SQL`, `SciPy`, `Statsmodels`, `Pandas`, `Matplotlib`, `Seaborn`, `Plotnine`

### 3. [Yelp Veterinary Data Pipeline and NLP Sentiment Mining](https://github.com/MLuftig/yelp-veterinary-sentiment-pipeline)

- **Problem:** Extracting meaningful sentiment signals from the multi-gigabyte Yelp Open Dataset to identify what drives customer satisfaction in the veterinary industry.
- **Solution:** Built a memory-efficient ETL pipeline using chunked JSON processing (100k-row batches) to filter 33,512 veterinary reviews from the full Yelp dataset, then applied TF-IDF vectorization (5,000 features) and a differential scoring method to isolate terms that distinguish low-star from high-star reviews.
- **Impact:** Identified billing/communication breakdowns (*"charged," "rude," "told," "money"*) as the dominant drivers of negative reviews, versus staff compassion and expertise (*"knowledgeable," "compassionate," "highly recommend"*) driving positive ones — visualized in a diverging bar chart for quick interpretation.
- **Tech Stack:** `Python`, `Jupyter`, `Pandas`, `NLTK`, `Scikit-Learn`, `Matplotlib`

---

## Apps

### 4. [Shelter Return Risk Predictor](https://github.com/MLuftig/shelter-risk-predictor)

- **Problem:** Making the shelter recidivism model actually usable by shelter staff, not just readable in a notebook.
- **Solution:** Built an interactive Streamlit app that loads the corrected, calibrated Random Forest model and lets users adjust length of stay, age, species, breed group, and intake reason to see a live, properly-calibrated return-risk probability.
- **Impact:** Turns a static ML model into a tool a non-technical shelter worker could use directly — try it live: [shelter-risk-predictor.streamlit.app](https://shelter-risk-predictor.streamlit.app/)
- **Tech Stack:** `Python`, `Streamlit`, `Scikit-Learn`, `Pandas`, `Joblib`

### 5. [Shelter Overflow Risk Forecaster](https://github.com/MLuftig/shelter-overflow-forecaster)

- **Problem:** Knowing that barometric pressure drops significantly affect shelter intake (per the moon-phase analysis) doesn't tell a shelter director how much operational risk that actually creates.
- **Solution:** Built a Monte Carlo simulation combining a two-component gamma mixture model of length-of-stay (capturing both typical short stays and a long-tail of hard-to-place animals) with a Negative Binomial regression quantifying the weather-intake relationship, to estimate real-time overflow risk from a 7-day pressure forecast.
- **Impact:** At a capacity near the shelter's steady-state population, a forecasted storm system nearly doubled the probability of at least one overflow day (34% → 61%) — and revealed that weather-driven risk is sharpest when capacity is already tight, disappearing almost entirely with sufficient buffer. Deployed as a live interactive tool: try it at [shelter-overflow-forecaster.streamlit.app](https://shelter-overflow-forecaster.streamlit.app/)
- **Tech Stack:** `Python`, `NumPy`, `SciPy`, `Streamlit`

### 6. [Shelter Medical Supply Forecaster](https://github.com/MLuftig/shelter-supply-forecaster)

- **Problem:** Shelter medical supply ordering is typically reactive — staff notice euthanasia-related consumables running low rather than anticipating demand ahead of time.
- **Solution:** Built a Monte Carlo simulation forecasting expected weekly euthanasia case volume from a temperature-adjusted Negative Binomial regression, allocating that volume across species and breed groups using real historical outcome proportions, then converting it into expected consumable usage (euthanasia solution, propofol, catheters, flush, body bags) with adjustable dosing defaults.
- **Impact:** Gives shelter staff a proactive, adjustable weekly usage estimate compared against current stock on hand, flagging likely shortages before they happen — try it live: [shelter-supply-forecaster.streamlit.app](https://shelter-supply-forecaster.streamlit.app/)
- **Tech Stack:** `Python`, `NumPy`, `SciPy`, `Streamlit`

---

## Technical Toolbox

- **Languages:** Python, SQL (SQLite, PostgreSQL)
- **Libraries & Frameworks:** Pandas, NumPy, Scikit-Learn, SciPy, Statsmodels, Seaborn, Matplotlib, Plotnine, NLTK, Streamlit
- **Core Competencies:** Relational Database Joins, Non-Parametric & Multivariate Hypothesis Testing, Monte Carlo Simulation
