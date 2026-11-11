# Final assignment analysis and work plan

Prepared 9 November 2026; updated 11 November after reviewing the Session 7 final assignment tutorial dated 29 October. This plan covers the supplied brief, tutorials, data dictionary, notebooks, and a preliminary check of both CSV files. It proposes the remaining work; it does not claim new model results or a proven financial return.

## What the assignment requires

Produce an executive business proposal supported by original EDA, external market research, and at least one appropriate machine learning or statistical model. The central chain of reasoning is:

**Client problem → evidence → model → business action → quantified benefit → pilot to verify the benefit.**

The brief does not provide numerical grading weights. Treat every stated requirement as necessary.

| Required item | Completion criterion |
|---|---|
| Business proposal | A specific decision, target customers, action, owner, and expected benefit |
| Original EDA | Multiple clear visualizations demonstrating client-specific problems |
| Model | Explicit model name, evaluation metric, and numerical score written on a slide; explain choice, construction, and insights |
| Market research | Relevant external evidence connected to the recommendation |
| Financial impact | Quantified revenue, cost, or risk effect with visible assumptions |
| Executive communication | Understandable without an ML background; logical consistency throughout |
| Slide submission | PDF, no more than 15 slides including title and references, at most 10 MB |
| Reproducible analysis | `.ipynb`, `.py`, or a ZIP of multiple analysis files |
| References | Citations on slides and a matching list in the portal; include generative AI chat history URL |
| File names | Slides and analysis named with the Omnicampus account name |
| Presentation language | English, explicitly required by the Session 7 tutorial |
| AI usage questionnaire | Complete the portal questionnaire shown in the Session 7 tutorial; the guide says AI usage does not affect the score |

**Deadline discrepancy:** the README and the shorter tutorial state 28 November 2026, **11:30 UTC = 5:30 PM in Dhaka**. The Session 7 guide, PDF page 6, instead states **11:00 UTC = 5:00 PM in Dhaka**. Do not assume either resolves the conflict without checking the portal or an instructor announcement. Use the earlier time as a precaution, not as a confirmed official correction. Aim to submit by **26 November**, retaining a buffer for either deadline. Resubmissions must include all required materials; only the latest submission is evaluated. Late additions are not accepted.

Submission portal from the brief: [Omnicampus final assignment](https://edu.omnicamp.us/en/courses/170/reports/125/). The portal has not been checked for subsequent announcements or changes.

## Current position

| Material | What is available | How to use it |
|---|---|---|
| `Final Assignment/README.docx` | Scenario, mandatory requirements, deadline, submission instructions | Submission authority |
| `final_assignment_tutorial.pdf` | Workflow and submission walkthrough | Supporting guidance; deadline and FAQ also inspected visually |
| Session 7 tutorial dated 29 October, in the lecture materials folder | Detailed issue/hypothesis/verification guidance and additional submission notes | Sharpen the reasoning and checklist; record its conflicting deadline |
| `Final Assignment/ENG_Company _A_ Dataset Overview.docx` | Partial dictionary, including the churn observation window | Definitions and a record of uncertainty |
| `Final Assignment/telecom/Record.csv` | 100,000 rows, 51 columns | Usage, billing, tenure, churn |
| `Final Assignment/telecom/Client.csv` | 100,000 rows, 50 columns | Account, handset, geography, household attributes |
| `Final Assignment/01_eda.ipynb` | Substantial EDA with saved outputs, interpretations, candidate hypotheses | Continue and correct this work |
| `Final Assignment/tutorial.ipynb` | Worked example including XGBoost and a stored accuracy of 0.6368 | Reference implementation; do not present its stored score as a newly verified result |

Independently checked: IDs are unique in both CSVs and their sets match. A validated one-to-one merge produces **100,000 rows and 100 columns: 98 potential features, target, and ID**. The target is 49,562 churners and 50,438 stayers. The dictionary defines churn as leaving **31–60 days after observation**, which supports acting before that outcome window.

Selected evidence already available:

- The EDA reports churn of about 65% at month 11 and 62% at month 12, compared with 29–40% at months 7–10. These are sample associations, not verified contract effects.
- Mean equipment age is 421 days among churners versus 363 days among stayers, independently reproduced from the CSVs.
- There are 1,615 zero-usage customers; 79.8% are churners in this sample, independently reproduced.
- Demographic missingness is substantial: vehicle count is missing for 49.4% and income for 25.4% of customers.
- There are 133 negative equipment ages, five negative monthly revenue values, and 23 negative recurring-charge values.
- The EDA reports that the highest-revenue 20% of customers contribute 42% of sample revenue. This motivates testing value-aware targeting; it does not prove that a particular targeting policy is profitable.

The main unfinished work is a defensible model comparison, a business-policy comparison, a financial scenario, external evidence, and the final presentation. A separate completed model notebook, deck, and reference list were not present in the supplied folder.

## Recommended proposal direction

**Test whether Company A can retain more contribution profit per unit of retention budget by prioritizing customers using both churn risk and customer value.**

Use churn as the initial binary classification target. It is explicitly defined, observable, and linked to a concrete retention decision. The business objective is incremental retained contribution after campaign costs. Model accuracy is a supporting measure.

Compare four policies under the same budget:

1. Random selection as a campaign baseline.
2. A simple operational rule using tenure and handset age.
3. Selection by predicted churn risk.
4. Selection by expected net retained contribution, combining risk, value, assumed intervention effectiveness, and cost.

Start with a low-cost contact and plan review. Treat handset upgrades as a separate, more expensive pilot option. Let measured evidence determine which intervention merits recommendation. Do not commit the proposal to universal discounts or upgrades before calculating break-even costs.

## What the Session 7 guide changes

Source: [Session 7 final assignment tutorial](</Volumes/Projects/GCI World_202609/03. Lecture Materials & Homework/Session7/GCI_World_Session7_Final_Assignment_Tutorial_20261029.pdf>). Page references below use the PDF's 1–50 page sequence, not the different numbers printed on the slides.

The guide reinforces the proposed churn/profit direction: page 38 explicitly offers increasing profit by reducing churn as a straightforward issue, while allowing other issues supported by the supplied data. It does not make churn compulsory or establish handset upgrades as effective. There is no reason to restart the topic.

Its main contribution is a clearer three-part test: an important issue, a concrete solution hypothesis, and a way to verify it (page 22). Page 31 distinguishes broad EDA used to discover the issue from focused EDA used to investigate a hypothesis. The existing `01_eda.ipynb` largely provides the first stage; the next work should test specific claims rather than expand the general survey.

Frame the proposed business issue as: **Which customers should receive a limited retention budget, and what action could yield positive incremental contribution?** Whether Company A currently misallocates that budget is unknown; do not invent a broken client process. Map the proposed workflow and stakeholders, and compare it with plausible simple alternatives.

Use these hypotheses to structure the next analysis:

| Hypothesis | Evidence needed | Response if unsupported |
|---|---|---|
| Tenure, equipment age, and engagement identify useful risk segments | Focused segment comparisons with counts, uncertainty, and checks within other relevant groups | Drop unsupported segment narratives |
| A multivariate model improves selection over a simple tenure/handset rule | Validation-set lift and churn capture at matched budgets | Prefer the simple rule or state that ML adds little value |
| Value-aware selection improves financial outcomes over risk-only selection | Matched-budget policy comparison, contribution assumptions, and sensitivity analysis | Retain risk-only targeting or revise costs and eligibility |
| The proposed offer prevents sufficient churn to cover costs | An explicit break-even effect and a future randomized pilot | Stop or revise the intervention if the pilot fails |

Page 39 clarifies that actual client feedback is unavailable for this assignment. The submission should therefore show a justified proposal, projected profit, limitations, and a continuing test-and-update process. A designed pilot is appropriate; a completed real-world campaign is not required. Revisit the hypothesis when verification fails, as the workflow on page 20 recommends.

Additional checks from pages 17 and 43–48: complete the AI questionnaire, use English, keep charts in the presentation itself, explain jargon, make slide transitions clear, and keep the proposal grounded in the supplied company/data. The guide says detailed grading rubrics will not be released and points back to README section 2. Keep the requirement checklist rather than inventing grading weights. Its mention of outstanding-student examples is an announcement; no example submission is included in this PDF.

## Corrections needed before modeling

1. **Separate observation from explanation.** Rename “contract cliff” to “tenure risk spike” unless contract dates or terms can be verified. A tenure pattern does not establish an actual renewal date, and cross-sectional data cannot establish the best earlier intervention month.
2. **Treat the sample churn rate carefully.** Near-balanced classes suggest selected sampling but do not prove its mechanism. Do not claim Company A loses half its customers. External churn rates provide scenarios, not Company A's true rate. Any prior-probability correction requires explicit assumptions about sampling and comparability.
3. **Resolve feature meanings conservatively.** The dictionary describes `change_mou` and `change_rev` as percentage changes, while the EDA interprets them as absolute differences. Keep their units unconfirmed unless validated. Do not decode credit classes as an ordered scale or treat every `U` as missing; meanings depend on the field.
4. **Audit availability at scoring time.** Weak single-feature AUC cannot rule out leakage. Check feature windows, identifiers, duplicates, and any information generated after observation. Document unresolved timing limitations.
5. **Do not infer intervention effects from associations.** Older phones and lower churn after apparent upgrades do not prove upgrades prevent churn. The data has no randomized offers or treatment outcomes.
6. **Use justified cleaning rules.** Negative equipment age can be marked missing. Negative billing values may be legitimate adjustments, so investigate and test alternatives rather than automatically declaring them errors. Sparsity alone is insufficient reason to discard `recv_sms_Mean`.
7. **Confirm financial units and population.** The dictionary does not establish currency or whether revenue is per line, customer, or household. Label any USD assumption. Do not multiply revenue by household lines without confirming the unit, or scale this sample directly to Company A's customer base.
8. **State the historical limitations.** US region names support a US market context, but the observation year is unknown. Handset and usage fields suggest historical data. Contemporary market reports are contextual comparisons rather than validation of the dataset's period or technology.

## Work packages and completion gates

### 1. Finalize the evidence and market context

**Target: 9–11 November.**

- Preserve the raw files and current notebooks. Make analysis paths work from the documented project location.
- Add an assumptions register: definitions, units, sampling, observation period, financial inputs, and treatment assumptions.
- Correct the EDA interpretations above. Select three or four strong charts, with segment counts and uncertainty, rather than adding many exploratory plots.
- Collect three to five primary sources on telecom competition, retention economics, and device or service relationships. Record publication date, metric definition, claim supported, URL, and comparability limits.
- Freeze the business question and the initial feature list.
- Write the hypotheses and their rejection criteria using the Session 7 table above. Map who scores customers, approves the budget, contacts customers, and measures outcomes; label this as a proposed workflow where Company A's actual process is unknown.

**Gate:** A one-paragraph problem statement, a cited market rationale, and a shortlist of actionable findings. Keep alternative explanations visible.

### 2. Build reproducible preparation and validation

**Target: 12–14 November.**

- Create `02_modeling.ipynb` with data validation, deterministic cleaning, and fixed seeds.
- Use a fixed stratified 60/20/20 train/validation/test split if no dates or groups suitable for better separation are available. Fit imputers, encoders, feature selection, and scaling on training data only. Use validation data for model and policy choices.
- Existing EDA examined the entire dataset; disclose that exposure. Freeze all further choices before final test evaluation, and avoid claiming a pristine external validation. A prospective pilot remains necessary.
- Drop `Customer_ID` from predictors. Initially exclude `ethnic` in line with the existing EDA decision. Compare a behavior/account/handset feature set with a broader feature set only if it adds useful, defensible information.
- For logistic regression, use numeric imputation and scaling plus categorical one-hot encoding. For a boosted tree, use suitable missing-value and categorical handling.
- Test a small feature set: equipment age relative to tenure, explicit zero-usage and missing-usage flags, tenure-window indicators, and carefully defined usage or call-quality ratios. Guard denominators and document the observation windows. Avoid naming a tenure feature “contract expiry” without evidence.

**Gate:** A restart-and-run-all preparation pipeline with disjoint splits, no ID predictors, and preprocessing fitted without validation/test data. [Scikit-learn's leakage guidance](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage) supports this workflow.

### 3. Compare models and targeting policies

**Target: 15–18 November.**

- Run a majority-class dummy baseline, logistic regression, and one gradient-boosted tree model. XGBoost is a reasonable first candidate because the tutorial already uses it. Keep tuning modest.
- Report ROC-AUC for ranking, precision and recall at the top 10% and 20%, lift over random selection, and accuracy/confusion matrix at a validation-selected threshold.
- For value-aware policies, report the share of observed churn-associated revenue captured at a fixed contact budget. Explicitly distinguish this proxy from preventable loss or realized profit.
- Select the model and campaign cutoff using validation results and business cost assumptions. Evaluate the frozen selection once on the test split. Add uncertainty intervals for the main comparison.
- If a hypothesis fails on validation data, revise it before freezing the final test evaluation. Preserve negative findings and prefer a simpler solution if ML does not improve the business decision.
- Explain model signals with held-out permutation importance or another documented method. Treat explanations as predictive associations.
- If probabilities enter a financial formula, assess calibration. Any deployment base-rate scenario needs a separate, justified adjustment; sample calibration alone does not establish real-world calibration.

**Gate:** One results table with model names, metrics, scores, split sizes, and policy comparisons. No promised AUC target and no borrowed tutorial score.

### 4. Quantify the business case and design the pilot

**Target: 19–21 November.**

Create `03_business_case.ipynb` or a clearly separated section of the final analysis. Distinguish measured inputs from external benchmarks and scenario assumptions.

Use a transparent equation:

**Expected net benefit = sum across targeted customers of (absolute churn reduction × contribution value of retained service − expected intervention cost) − fixed campaign cost.**

- Define the churn measurement window and retained-service horizon separately. Use contribution margin, rather than calling all revenue profit.
- Without treatment data, an assumed absolute churn reduction can be expressed as untreated churn probability × fraction of otherwise-occurring churn prevented. Neither intervention effectiveness nor offer acceptance is learned by the churn model.
- Include contact expense, expected redeemed incentives, handset subsidy where relevant, and fixed operating expense. Avoid charging redemption costs incorrectly or counting the same benefit twice.
- Show conservative/base/optimistic scenarios and break-even intervention effectiveness or allowable cost. Vary deployment churn, margin, retention duration, and intervention cost. Prefer results per 10,000 eligible customers to an unsupported company-wide total.
- If reweighting the selected sample to a hypothetical deployment prevalence, also reweight policy evaluation and the targeted fraction; do not simply multiply sample precision by a new average churn rate.
- Propose randomized treatment and control groups within eligible risk/value strata. Specify owner, eligibility, offer, sample-size calculation, the 31–60-day churn outcome, incremental margin KPI, and stop/expand criteria.

**Gate:** A reproducible sensitivity table and a pilot whose success is incremental contribution versus control. A risk model does not establish who is most persuadable; uplift modeling can follow when treatment data exists.

### 5. Build the executive deck

**Target: 22–24 November.**

Use the following 15-slide budget. Every substantive title should state the conclusion supported by the final analysis; do not write optimistic conclusions before results exist.

| Slide | Purpose and evidence |
|---|---|
| 1 | Title and the requested business decision |
| 2 | Executive recommendation, expected scenario range, and pilot ask |
| 3 | Market context with cited external evidence |
| 4 | Dataset, target horizon, and key representativeness limitations |
| 5 | Tenure and handset findings with segment sizes |
| 6 | Engagement/usage finding and why it suggests outreach |
| 7 | Customer value concentration and the budget allocation problem |
| 8 | Proposed scoring-to-action workflow, ownership, and timing |
| 9 | Model setup: preprocessing, splits, models, and rationale |
| 10 | Model comparison with explicit names, metrics, and actual scores |
| 11 | Fixed-budget policy comparison using lift/capture and value measures |
| 12 | Business-case equation, cost assumptions, and scenario results |
| 13 | Sensitivity and break-even analysis |
| 14 | Randomized pilot, risks, decision criteria, and how feedback revises the proposal |
| 15 | References matching the on-slide citations |

Use approximately six to eight purposeful visuals across the deck, with figures visible on the slides themselves. Write the presentation in English, explain specialist terms, and ensure each slide follows clearly from the preceding one. Avoid an agenda or divider slides unless they replace an existing slide. Keep technical detail sufficient to explain validity while reserving full code and diagnostics for the notebook.

**Gate:** At most 15 slides with a clear decision and a consistent path from evidence to action to impact.

### 6. Reproduce, package, and submit

**Target: 25–26 November; buffer 27–28 November.**

- Restart the runtime and run the final notebook(s) from top to bottom. Record dependencies, paths, seeds, and instructions. Ensure no outputs rely on hidden state.
- Prefer one consolidated account-named notebook; use an account-named ZIP if multiple files are necessary. Explain where to place the supplied CSVs.
- Confirm every slide number matches the final notebook and every citation has a matching portal entry. Add the generative AI chat history URL as required by the brief. Review and understand the analysis and write the final conclusions in your own voice.
- Complete the AI usage questionnaire in the submission portal and verify the current deadline against the two conflicting local sources. Keep the 26 November submission target regardless.
- Export the slides to PDF and visually inspect every page for clipping, small text, broken symbols, and chart legibility. Verify page count and file size.
- Replace all account-name placeholders with the actual Omnicampus account name.
- Upload the PDF, analysis, and reference list together. Confirm submission success and retain a local copy. Any resubmission must contain all materials again.

**Gate:** Reproducible analysis, PDF at most 15 pages and 10 MB, matching references, correct filenames, and a confirmed submission before the deadline.

## Research starting points

These primary sources were checked while preparing the plan. They are starting points, not a completed market review:

- [AT&T 2025 results, published 28 January 2026](https://about.att.com/story/2026/4q-earnings-2025.html): contemporary operator performance and churn context. Do not transfer its rate directly to Company A.
- [AT&T third-quarter 2025 SEC filing](https://www.sec.gov/Archives/edgar/data/732717/000073271725000171/t-20250930.htm): defines reported churn as an average of monthly cancellation rates and discusses device-financing periods and competitive pressure. This supports market plausibility, not proof of Company A's contract mechanism.
- [Scikit-learn common pitfalls and leakage guidance](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage): supports training-only preprocessing and appropriate evaluation.

## Immediate next action

Correct the unsupported interpretations in `01_eda.ipynb`, write the one-paragraph business problem and assumptions register, then create `02_modeling.ipynb` with fixed validation rules. The highest-value next output is a trustworthy model-and-policy comparison that can support the financial case.
