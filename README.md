# Oral health and diabetes in US adults (NHANES 2013-2014)

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
- Validation:the data were split 80/20 into training and test sets (stratified, so both kept the same share of diabetes cases). The model learned from the training set only and was scored on the test set, which it had not seen. Because a single split can be lucky or unlucky, I also used 5-fold cross-validation, which trains and tests the model five times on different parts of the data and averages the AUC.

## Results
- Age, sex, BMI only: mean AUC 0.726 (SD 0.024, 5-fold cross-validation).
- Adding oral health variables: mean AUC 0.731 (SD 0.024).
- Adding oral health variables raised the mean AUC by only 0.005 (0.726 to 0.731), much less than the variation between folds (SD 0.024).I therefore cannot conclude that tooth counts improve prediction beyond age, sex and BMI.
- On a single 80/20 split, test AUC was 0.774, but this is based on about 105
  cases and is less reliable than the cross-validated estimate.
- At the usual 0.5 cut-off, sensitivity was only 0.03 (specificity 0.997). Only about 12.7% of people have diabetes, so the model rarely estimates a risk above 50% and labelled almost everyone as not having diabetes. Lowering the cut-off to the overall prevalence (0.127) raised sensitivity to 0.77 and lowered specificity to 0.67. The model is the same; the cut-off sets the balance between missed cases and false alarms.
- People with diabetes had fewer natural teeth on average (17.6 vs 21.2) but were also older (60.8 vs 53.0 years). Older age is linked to both tooth loss and diabetes, so age is a confounder and the raw difference in teeth partly reflects age. Including age in the model accounts for part of this, but not all of it.

## Limitations
- Cross-sectional data: this shows association, not early detection or causation.
- NHANES survey weights were not used, so results are not nationally representative.
- Diabetes was defined by HbA1c only; treated, well-controlled diabetes may be missed.
- "Teeth lost to dental disease" combines caries and periodontal causes.
- Natural teeth and teeth lost overlap, so their coefficients should not be
  interpreted separately.
- About 350 people with missing data were excluded.
- - Only tooth-count variables were used; gum disease measures from the periodontal exam were not analysed.
- Results come from a single NHANES cycle (2013-2014), odds ratios are crude (no confidence intervals), and the model was not tested on a separate dataset.

## Next steps
Add periodontal measures (pocket depth, attachment loss) and compare models.

## How to run
Open the notebook in Google Colab and choose Runtime > Run all. It downloads the data itself.

## About
Dr Sharanya Sreekumar, BDS, MDS (Public Health Dentistry). I built this project to gain practical experience in training and validating prediction models. Python and scikit-learn guidance was supported by an AI assistant (Claude). All analysis decisions and interpretations were reviewed and explained by me.


All analysis decisions and interpretations were reviewed and explained by me.
