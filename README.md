Micah Luftig
Data Scientist | Licensed Veterinary Technician | MS

I am an LVT with 15+ years of experience primarily in emergency/critical care medicine, and I fell in love with exploring data while working on my graduate degree which focused heavily on biometry.

Connect with me: [LinkedIn](https://www.linkedin.com/in/micah-luftig) | m.luftig24@gmail.com

## Animal Shelter Data Science

### Projects

**1. Animal Shelter Recidivism Prediction**

**Problem:** Identifying key risk variables that cause adopted pets to be rapidly returned to local shelter facilities within a 30-day window.

**Solution:** Developed an end-to-end Python pipeline utilizing SQL joining for feature engineering and a Random Forest classification model, including a documented correction of an early target-leakage issue in the model's training data.

**Impact:** Found that an animal's age and species are the strongest predictors of return risk — not length of stay, which an earlier version of the model had mistakenly identified as dominant. Dogs return at roughly 2.7x the rate of cats, and the corrected model achieves 76% recall on true return cases. Extended to a second, independent shelter (Bloomington, IN) to test generalization: the model transferred only partially (AUC dropped from 0.71 to 0.64), and a Bloomington-native model revealed the two shelters are driven by meaningfully different factors — length of stay dominates there instead of age/species.

**Tech Stack:** Python, SQL, Scikit-Learn, Pandas, Matplotlib, Seaborn

**2. Environmental and Lunar Influences on Shelter Volume**

**Problem:** Myth-busting the long-held veterinary belief — one I personally heard repeated throughout 15+ years of ER practice — that lunar cycles impact patient surge volumes, while isolating real weather triggers for both intake volume and shelter mortality.

**Solution:** Built a multi-layer SQL data engineering extraction pipeline in Python to merge historical shelter data with localized climatology logs, using non-parametric hypothesis testing followed by multivariate regression to properly isolate independent weather effects.

**Impact:** Debunked the "Full Moon Effect" via robust non-parametric Kruskal-Wallis testing. A follow-up multivariate analysis found that "feels-like" temperature — not barometric pressure — is the primary independent driver of both intake volume and mortality; pressure's apparent effect in isolation was largely a statistical proxy for temperature.

**Tech Stack:** Python, SQL, SciPy, Statsmodels, Pandas, Matplotlib, Seaborn, Plotnine

**3. Yelp Veterinary Data Pipeline and NLP Sentiment Mining**

**Problem:** Extracting meaningful sentiment signals from the multi-gigabyte Yelp Open Dataset to identify what drives customer satisfaction in the veterinary industry.

**Solution:** Built a memory-efficient ETL pipeline using chunked JSON processing (100k-row batches) to filter 33,512 veterinary reviews from the full Yelp dataset, then applied TF-IDF vectorization (5,000 features) and a differential scoring method to isolate terms that distinguish low-star from high-star reviews.

**Impact:** Identified billing/communication breakdowns ("charged," "rude," "told," "money") as the dominant drivers of negative reviews, versus staff compassion and expertise ("knowledgeable," "compassionate," "highly recommend") driving positive ones — visualized in a diverging bar chart for quick interpretation.

**Tech Stack:** Python, Jupyter, Pandas, NLTK, Scikit-Learn, Matplotlib

### Apps

**4. Shelter Return Risk Predictor**

**Problem:** Making the shelter recidivism model actually usable by shelter staff, not just readable in a notebook.

**Solution:** Built an interactive Streamlit app that loads two independently-trained, calibrated Random Forest models — Austin and Bloomington — and predicts return risk for the same animal profile through both side by side, so users can see how the two shelters' different underlying drivers change the prediction.

**Impact:** Turns a static ML model into a tool a non-technical shelter worker could use directly, while making the cross-shelter finding tangible in real time rather than just a static chart — try it live: shelter-risk-predictor.streamlit.app

**Tech Stack:** Python, Streamlit, Scikit-Learn, Pandas, Joblib

**5. Shelter Overflow Risk Forecaster**

**Problem:** Shelter intake volume is inherently random, and prior work in this portfolio (the moon-phase & weather analysis) identified that "feels-like"/average temperature is a statistically significant driver of intake surges — but a p-value alone doesn't tell a shelter director how much that actually matters operationally, or whether a model built at one shelter reflects another.

**Solution:** Built a Monte Carlo simulation combining a two-component gamma mixture model of length-of-stay (a clearly bimodal distribution at both shelters — most animals turn over quickly, but a smaller subpopulation stays for months; Bloomington's long-stay rate is more than double Austin's) with a Negative Binomial regression per city, isolating temperature as the real driver after confirming pressure's apparent effect disappears once temperature is controlled for (Austin p=0.311; Bloomington's residual pressure effect was smaller but not fully explained, p=0.046 — an honest nuance documented rather than smoothed over). Users enter a ZIP code and both cities' independently-trained models run against the same real weather, shown side by side.

**Impact:** At each city's own capacity, a forecasted heat wave more than doubled the probability of at least one overflow day versus an average week (Austin: 47.4% → 85.6%, capacity 900; Bloomington: 2.5% → 24.3%, capacity 450) — and confirmed the temperature-driven relationship replicates across both shelters despite very different scale and per-degree sensitivity (Bloomington's intake is more than twice as temperature-sensitive per degree as Austin's). Deployed as a live interactive tool: try it at shelter-overflow-forecaster.streamlit.app

**Tech Stack:** Python, NumPy, SciPy, Requests, Streamlit

**6. Shelter Medical Supply Forecaster**

**Problem:** Shelter medical supply ordering is typically reactive — staff notice euthanasia-related consumables running low rather than anticipating demand ahead of time, and it's unclear whether a weather-mortality relationship found at one shelter would hold at another.

**Solution:** Built a Monte Carlo simulation comparing two independently-trained, temperature-adjusted Negative Binomial models side by side — Austin and Bloomington — each allocating expected mortality across species and breed groups using real historical proportions, then converting it into expected consumable usage (euthanasia solution, propofol, catheters, flush, body bags) with adjustable dosing defaults. Users enter a ZIP code to pull a live 7-day forecast, applied to both models at once.

**Impact:** Gives shelter staff a proactive, adjustable weekly usage estimate compared against current stock on hand, flagging likely shortages before they happen — and confirmed the weather-mortality relationship independently replicates at a second, much smaller shelter in a different climate, unlike a related recidivism model that didn't transfer well. Try it live: shelter-supply-forecaster.streamlit.app

**Tech Stack:** Python, NumPy, SciPy, Requests, Streamlit

## Insurance & Actuarial Risk

Applying this portfolio's core techniques — Monte Carlo simulation, probability calibration correction, and rigorous real-data verification — outside the animal shelter domain.

### Projects

**7. Pet Insurance Risk & Pricing Analysis**

**Problem:** Testing whether real, cited veterinary breed-disease research can meaningfully improve pet insurance pricing beyond flat demographic factors (species/breed/age), and whether the current premium structure actually tracks risk.

**Solution:** Built a breed-predisposition lookup table sourced from cited veterinary literature and independently evaluated for clinical plausibility rather than applied as-is, tested it in a calibrated Random Forest hurdle model, caught and corrected two related bugs along the way (a probability-calibration issue and a stale-variable reference bug — both documented in full in the README's Model Correction Note), then built a Monte Carlo portfolio simulation, a breed-level pricing fairness audit, and a survival analysis of time-to-first-claim.

**Impact:** Found a real, honest ceiling on individual-level claims prediction (AUC 0.58) — age and species dominate, and most flagged conditions are late-onset chronic disease that wouldn't be expected to drive first-year claims. A follow-up survival analysis, using a completely different technique (Cox Proportional Hazards), independently confirmed the same ceiling (concordance 0.54) — two separate methods arriving at the same honest conclusion. The same calibrated model, applied at the portfolio level, forecasts total annual cost within 0.04% of real historical data. A separate pricing audit found a real, size-correlated gap between charged premium and modeled risk, and closes with two specific, sourced recommendations for stakeholders (a missing indoor/outdoor variable for cats, and a real, documented cat-insurance coverage gap worth a product question).

**Tech Stack:** Python, Scikit-Learn, SciPy, Joblib, lifelines

### Apps

**8. Pet Insurance Cost Simulator**

**Problem:** Making the risk model above usable by an individual, not just a portfolio-level reserving exercise.

**Solution:** Built an interactive Streamlit app that runs the same calibrated model and Monte Carlo method against a single user-specified pet profile (species, breed, age), showing a real cost-range simulation — typical/worst-case/extreme-worst-case scenarios — plus how that range shifts across the pet's lifetime.

**Impact:** Surfaces a genuinely counterintuitive finding directly to a user: for most pets, the most likely first-year outcome is $0 — not a weak result, but the actual statistical shape of why insurance exists, paired transparently with a real, quantified worst-case tail. Try it live: pet-insurance-cost-simulator.streamlit.app

**Tech Stack:** Python, Streamlit, Scikit-Learn, Joblib, Matplotlib

**9. Pet Insurance Portfolio Dashboard**

**Problem:** Every tool above answers a single-case question (one pet, one prediction) — there was no way to see the portfolio's findings together, at a glance, the way a reserving or pricing team actually needs to.

**Solution:** Built a multi-panel Streamlit dashboard reusing the same calibrated model and validated computations from the analysis repo — population breakdown, real claim severity distribution, the Monte Carlo portfolio forecast as an interactive chart, the breed-level pricing audit as a color-coded bar chart, and Kaplan-Meier survival curves — all on one screen, nothing recalculated with different assumptions.

**Impact:** Turns five separate, text-heavy findings into a single interactive view a stakeholder could actually explore — try it live: insurance-portfolio-dashboard.streamlit.app

**Tech Stack:** Python, Streamlit, Plotly, Scikit-Learn, Joblib, lifelines

## Market & Financial Analysis

Applying this portfolio's core habit — testing whether a clean, intuitive story survives contact with real, cited data — to corporate financial filings and market pricing.

### Projects

**10. Did COVID Create a Durable Shift in the Pet Economy? (Retail, Insurance, Food & Diagnostics)**

**Problem:** Testing whether pandemic-era demand shifts across the pet economy — retail (Chewy/Petco), insurance (Trupanion), food (Hill's), and veterinary diagnostics (IDEXX) — represent a lasting structural change or a temporary shock that mostly reverted, and whether the stock market itself believes the shift stuck.

**Solution:** Built a three-part analysis using real, primary-source SEC EDGAR filings and 10-K data throughout. Started with a true quarterly growth-rate comparison and trend-vs-actual revenue test for Chewy and Petco, including an exact (not estimated) derivation of missing Q4 figures via the accounting identity. Extended to three more categories (Trupanion via live SEC API, Hill's and IDEXX via manually-transcribed 10-K segment data), then added a live stock-price analysis (via yfinance) to test a genuinely different question — not whether revenue grew, but whether the market priced in a durable shift — kept as a deliberately separate thread from the revenue analysis rather than blended into one verdict.

**Impact:** Found no single story holds across the pet economy. Petco shows a genuine, durable revenue shift; Chewy's picture is ambiguous due to an unrealistic 51%/year pre-COVID baseline; Hill's and IDEXX both show real, growing revenue durability, but the stock market has only rewarded that with a matching valuation premium in IDEXX's case — Chewy and Trupanion both grew revenue substantially since 2020 yet still trade below their pre-COVID stock price. An unresolved data anomaly (Trupanion's FY2019→FY2020 revenue drop) is flagged as an open question rather than smoothed into a finding.

**Tech Stack:** Python, Pandas, NumPy, SciPy, Matplotlib, Requests (SEC EDGAR API), yfinance

## Technical Toolbox

**Languages:** Python, SQL (SQLite, PostgreSQL)

**Libraries & Frameworks:** Pandas, NumPy, Scikit-Learn, SciPy, Statsmodels, Seaborn, Matplotlib, Plotly, Plotnine, NLTK, Streamlit, Joblib, lifelines, Requests, yfinance

**Core Competencies:** Relational Database Joins, Non-Parametric & Multivariate Hypothesis Testing, Monte Carlo Simulation, Probability Calibration, Survival Analysis
