# Subscription Funnel Analysis

## Project Overview

This project analyzes the subscription conversion funnel of a freemium mobile photo editing application available on iOS and Android platforms.

The goal is to understand user behavior across the funnel, identify key drop-off points, and generate actionable product insights to improve subscription conversion and user engagement.

The analysis is based on behavioral data collected between **November 6–19, 2023**.

---

## Business Context

The application follows a freemium model:

* Free users can access basic editing features
* Premium features (HD portrait, object removal, stickers, beautify effects) require a subscription

The company operates across four markets:

* Brazil (BR)
* Vietnam (VN)
* Egypt (EG)
* Germany (DE)

The main objective is to analyze how users move from app install → registration → product usage → subscription purchase.

---

## Datasets

Two datasets were used in this project:

### 1. app_open_data.csv

Contains app open and session-level information:

* app opens
* install flag
* platform (Android / Apple)
* country
* user and device identifiers

### 2. event_data.csv

Contains in-app behavioral events:

* registration events
* editor interactions
* subscription offer views
* export actions
* subscription purchases

### Data Access

The datasets are hosted externally due to file size considerations:

**Download link:** [https://drive.google.com/drive/folders/1MjAynknBPM24RZVuDJbN1MeJzTe8fqkh?usp=drive_link]

To reproduce the analysis:

* Download both files
* Place them in the same directory as the notebook
* Run the notebook from top to bottom

---

## Tools & Technologies

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Plotly
* SciPy

---

## Project Structure

```
├── Subscription_Funnel_Analysis.ipynb
├── README.md
```

*(Data files are stored externally and not included in the repository.)*

---

## Analysis Workflow

### 1. Funnel Construction

Built the end-to-end user funnel:

* app_open
* registration_open
* registration_done
* create_flow_open
* editor_open
* subscription_offer_open
* object_export
* subscription_done

Computed:

* unique users/devices at each stage
* stage-to-stage conversion rates
* overall funnel conversion

---

### 2. Segmentation Analysis

Funnel performance was analyzed across:

* Platforms (Android vs iOS)
* Countries (BR, VN, EG, DE)

Identified differences in:

* conversion rates
* drop-off points
* user engagement behavior

---

### 3. Registration Analysis

* Measured completion rate of registration flow
* Compared performance across platforms and countries
* Investigated potential friction points in onboarding

---

### 4. Behavioral Analysis

* Analyzed sources leading to subscription offer exposure
* Examined session depth before paywall appearance
* Studied relationship between engagement and conversion

---

### 5. User Type Analysis

* Compared new vs returning users using `is_first_app_open`
* Evaluated differences in:

  * funnel progression
  * engagement level
  * conversion probability

---

## Key Findings

* The funnel is highly non-linear: ~77% of users reach the editor without registering, meaning registration is not required for core product usage.

* The largest drop-off occurs at the earliest stage (app_open → registration_open), with ~89% of users not entering registration, indicating weak early activation or low perceived value of sign-up.

* Monetization performance is very low, with ~92 subscriptions from ~32K active devices (~0.3% overall conversion). The biggest leakage occurs at the paywall stage (~0.8% conversion from offer views).

* Strong platform effect: iOS users convert significantly better than Android users, especially at the paywall stage.

* Clear country-level differences: Germany shows the highest per-user conversion efficiency, Brazil leads in total volume, and Egypt shows the lowest conversion, likely due to price sensitivity.

* Registration is a major friction point with ~48% completion rate among users who start the flow.

* High-intent behavior significantly increases conversion: users interacting with premium features (e.g., background removal, object editing) convert much more than users exposed to generic paywall triggers.

* Engagement depth is positively correlated with subscription conversion: users performing more editing actions before paywall exposure are more likely to subscribe.


---

## Recommendations

* Shift paywall triggers to **high-intent moments** (e.g., when users attempt premium features like background removal, object editing, or advanced tools) instead of early-stage screens such as photo selection.

* Redesign onboarding and registration flow to reduce friction by introducing **social login (Google / Apple), fewer required fields, and optional guest mode with deferred registration**, aiming to increase registration completion.

* Implement **market-specific pricing strategy**, especially for price-sensitive regions (e.g., Egypt and Vietnam), using localized or PPP-adjusted pricing to improve conversion rates.

* Delay monetization prompts until users demonstrate engagement by performing multiple editing actions within a session, leveraging the observed relationship between **session depth and conversion probability**.

* Prioritize A/B testing of paywall timing and placement to validate impact on subscription conversion and overall revenue performance.


---

## Limitations

* The analysis is based on a relatively short observation window (2 weeks), which may not capture seasonal effects, marketing campaigns, or longer-term user behavior patterns.

* The total number of conversions is very small (~92 subscriptions), which limits statistical confidence in some segmented analyses and may lead to higher variance in results.

* Full end-to-end user tracking is not possible due to minimal overlap between `app_open_data` and `event_data`, preventing a unified funnel at the individual user level.

* The dataset lacks revenue and pricing variation data, so it is not possible to evaluate revenue impact or perform price elasticity analysis directly.

* External factors such as acquisition channels, ad campaigns, and attribution sources are not included, limiting understanding of traffic quality differences.


---

## Future Work

* Extend the analysis to a longer time period (30–90 days) to capture seasonality, user lifecycle effects, and potential marketing campaign impacts.

* Build cohort-based retention analysis (D1, D7, D14) to better understand how early engagement influences long-term subscription probability.

* Design and evaluate A/B tests for paywall timing, placement, and messaging to validate the impact of contextual monetization strategies.

* Perform statistical significance testing across platforms and countries to confirm whether observed conversion differences are robust or due to sampling noise.

* Develop a predictive model to estimate subscription probability based on early behavioral signals (session depth, feature usage, and interaction patterns).

* Analyze acquisition channels (if available) to identify high-quality traffic sources and their downstream conversion performance.

---

## Author

Erik Shahbazyan

