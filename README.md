# Data Preprocessing and Analysis

A Python data preprocessing pipeline applied to a forestry stem measurement dataset, built as part of a Data Science Programming university assignment.

This project covers the full preprocessing workflow: inspection, validation, missing data handling, feature engineering, and encoding — preparing a raw dataset for machine learning.

## What This Project Does

**Inspection**
- Loaded and inspected data types, shape, and first rows
- Renamed misspelled columns (`Dai_cm` → `Diameter_cm`, `Leght_m` → `Length_m`)
- Used a missingness heatmap to identify structural (non-random) missing data

**Data Validation**
- Validated moisture percentage (0–100 range only)
- Converted `MeasurementDate` to datetime format
- Checked all categorical columns for inconsistencies
- Removed duplicate rows using a composite key
- Removed out-of-scope non-stem rows based on metadata
- Recalculated `IsOutlier` flags using the IQR method
- Fixed a dry/wet weight constraint violation using global median

**Filling Missing Data**
- `%Moisture` — filled with global median (no correlation found with other columns)
- `Diameter_cm` — filled with grouped median per layer (right-skewed, outlier-resistant)
- `Length_m` — filled with grouped median per layer; D0 set to 0 by definition
- `LogVolume_m3` — recalculated using the cylinder formula after discovering length was recorded in cm not meters
- `MoistureClass` / `DiameterClass` — filled using quantile binning (`qcut`) for balanced distribution

**Feature Engineering**
- Ordinal encoding for `DiameterClass` and `MoistureClass` (ordered categories)
- One-hot encoding for `SoilType` (nominal, no ranking)
- Min-Max normalization for `Altitude_m` (right-skewed)
- Standardization for `Slope_deg` (normally distributed)
- Engineered `CrossSectionArea_cm2` from diameter using π r²
- Engineered `AltitudeBand` column using `qcut` for equal-frequency altitude grouping

## Tools & Libraries

- Python, Pandas, NumPy
- Matplotlib, Seaborn
