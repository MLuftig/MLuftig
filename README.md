# Micah Luftig

### Data Scientist | Licensed Veterinary Technician | MS

I am an LVT with 15+ years of experience primarily in emergency/critical care medicine, and I fell in love with exploring data while working on my
graduate degree which focused heavily on biometry.

**Connect with me:** [LinkedIn](https://www.linkedin.com/in/micah-luftig/) | <m.luftig24@gmail.com>

---

## Featured Projects

### 1. [Animal Shelter Recidivism Prediction](https://github.com/MLuftig/animal-shelter-recidivism-prediction)

- **Problem:** Identifying key risk variables that cause adopted pets to be rapidly returned to local shelter facilities within a 30-day window.
- **Solution:** Developed an end-to-end Python pipeline utilizing SQL joining for feature engineering and an optimized Random Forest classification model.
- **Impact:** Discovered that length of stay had a 55% predictive impact on canine recidivism, enabling the pipeline to achieve a 61% model recall rate to catch true risk cases.
- **Tech Stack:** `Python`, `SQL`, `Scikit-Learn`, `Pandas`, `Matplotlib`, `Seaborn`

### 2. [Environmental and Lunar Influences on Shelter Volume](https://github.com/MLuftig/moon-phase-weather-shelter-analysis)

- **Problem:** Myth-busting the long-held veterinary belief that lunar cycles impact patient surge volumes, while isolating real weather triggers.
- **Solution:** Built a multi-layer SQL data engineering extraction pipeline in Python to merge historical shelter data with localized climatology logs.
- **Impact:** Debunked the "Full Moon Effect" via robust non-parametric Kruskal-Wallis testing and isolated barometric pressure drops as highly statistically significant (p = 2.58e-23) volume drivers.
- **Tech Stack:** `Python`, `SQL`, `SciPy`, `Pandas`, `Matplotlib`, `Seaborn`

### 3. [Yelp Veterinary Data Pipeline and NLP Sentiment Mining](https://github.com/MLuftig/yelp-veterinary-sentiment-pipeline)

- **Problem:** Extracting meaningful sentiment signals from the multi-gigabyte Yelp Open Dataset to identify what drives customer satisfaction in the veterinary industry.
- **Solution:** Built a memory-efficient ETL pipeline using chunked JSON processing (100k-row batches) to filter 33,512 veterinary reviews from the full Yelp dataset, then applied TF-IDF vectorization (5,000 features) and a differential scoring method to isolate terms that distinguish low-star from high-star reviews.
- **Impact:** Identified billing/communication breakdowns (*"charged," "rude," "told," "money"*) as the dominant drivers of negative reviews, versus staff compassion and expertise (*"knowledgeable," "compassionate," "highly recommend"*) driving positive ones — visualized in a diverging bar chart for quick interpretation.
- **Tech Stack:** `Python`, `Jupyter`, `Pandas`, `NLTK`, `Scikit-Learn`, `Matplotlib`

### 4. [Shelter Return Risk Predictor](https://github.com/MLuftig/shelter-risk-predictor)

- **Problem:** Making the shelter recidivism model actually usable by shelter staff, not just readable in a notebook.
- **Solution:** Built an interactive Streamlit app that loads the trained Random Forest model and lets users adjust length of stay, age, species, breed group, and intake reason to see a live return-risk prediction.
- **Impact:** Turns a static ML model into a tool a non-technical shelter worker could use directly — try it live: [shelter-risk-predictor.streamlit.app](https://shelter-risk-predictor.streamlit.app/)
- **Tech Stack:** `Python`, `Streamlit`, `Scikit-Learn`, `Pandas`, `Joblib`

---

## Technical Toolbox

- **Languages:** Python, SQL (SQLite, PostgreSQL)
- **Libraries & Frameworks:** Pandas, NumPy, Scikit-Learn, SciPy, Seaborn, Matplotlib, NLTK
- **Core Competencies:** Relational Database Joins, Non-Parametric
