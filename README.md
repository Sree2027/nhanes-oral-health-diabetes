# nhanes-oral-health-diabetes# Oral health and diabetes in US adults (NHANES 2013-2014)

Personal learning project exploring whether simple oral health measures
add information to a diabetes prediction model.

## Question
Do tooth-count measures improve prediction of diabetes beyond age, sex and BMI?

## Data
NHANES 2013-2014 (US CDC), public and de-identified:
demographics (DEMO_H), glycohemoglobin (GHB_H), body measures (BMX_H),
oral health dentition exam (OHXDEN_H).
Source: https://wwwn.cdc.gov/nchs/nhanes/

## Methods
- Population: adults aged 30+ with an HbA1c result (n = 4,502); 4,150 had complete data.
- Outcome: diabetes = HbA1c >= 6.5% (12.7% of the analysis sample).
- Predictors: age, sex, BMI, number of natural teeth (of 28), teeth lost to
  dental disease, decayed teeth.
- HbA1c was NOT used as a predictor, to avoid data leakage.
- Model: logistic regression (scikit-learn).
- Validation: [explain in your own words: 80/20 split and 5-fold cross-validation, and why].

## Results
- Age, sex, BMI only: mean AUC 0.726 (SD 0.024, 5-fold cross-validation).
- Adding oral health variables: mean AUC 0.731 (SD 0.024).
- [Your interpretation: the gain was small and within the fold-to-fold variation.]
- On a single 80/20 split, test AUC was 0.774, but this is based on about 105
  cases and is less reliable than the cross-validated estimate.
- At a cut-off equal to the overall prevalence (0.127), sensitivity was 0.77 and
  specificity 0.67. [Explain why the default 0.5 cut-off gave sensitivity of only 0.03.]
- People with diabetes had fewer natural teeth on average (17.6 vs 21.2) but
  were also older (60.8 vs 53.0 years). [Explain why age matters here.]

## Limitations
- Cross-sectional data: this shows association, not early detection or causation.
- NHANES survey weights were not used, so results are not nationally representative.
- Diabetes was defined by HbA1c only; treated, well-controlled diabetes may be missed.
- "Teeth lost to dental disease" combines caries and periodontal causes.
- Natural teeth and teeth lost overlap, so their coefficients should not be
  interpreted separately.
- About 350 people with missing data were excluded.
- [for example, the periodontal exam excluded some people with
  heart conditions.]

## Next steps
Add periodontal measures (pocket depth, attachment loss) and compare models.

## How to run
Open the notebook in Google Cola and choose Runtime > Run all.
It downloads the data itself.
[Your name, background in public health dentistry, one line on why you did this.]
Python and scikit-learn guidance was supported by an AI assistant (Claude).
All analysis decisions and interpretations were reviewed and explained by me.
