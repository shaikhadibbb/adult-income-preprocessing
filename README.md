# test 3 data preprocessing

Submission for Assignment 3 (Test 03 – Data Preprocessing) using the UCI Adult Income dataset. No model training or machine learning was done, just the data cleaning pipeline.

## files in this repo
* `data_preprocessing.ipynb` - Jupyter notebook containing all the code cells, markdown explanations of my thought process, and seaborn/matplotlib graphs.
* `cleaned_adult_income.csv` - The final cleaned, scaled, and encoded dataset exported to a CSV file.

## what i did:
- **missing values**: UCI dataset has a weird issue where strings have leading spaces, so `'?'` was loaded as `' ?'`. I stripped all string columns first, then replaced with NaN. Used mode imputation to fill them since the columns (`workclass`, `occupation`, `native-country`) are categorical. 
- **duplicates**: dropped duplicate rows.
- **outliers**: used IQR method strictly on `age` and `hours-per-week`. I originally tried running IQR on all numeric features but it deleted all rows with capital gains (since most are 0, making Q1, Q2, and Q3 all 0, so IQR is 0). I only applied IQR to age and hours-per-week to save the useful data.
- **encoding**: 
  - One-hot encoded nominal features (dropped first column to avoid dummy trap).
  - Ordinal encoded the `education` column based on the class list.
  - Label encoded the binary target column (`income`).
- **scaling**: used `StandardScaler` on continuous columns so they all have mean 0 and std 1.
- **feature dropping**: dropped `fnlwgt` since it's just a census weight and useless for predicting individual income, and `education` because it's redundant with `education-num`.
- **skewness**: capital-gain and capital-loss were super skewed, so I log-transformed them using `np.log1p` before scaling.

The notebook is fully executed, so the output cells, boxplots, histograms, and the correlation heatmap are already saved inline.
