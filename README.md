Bangladesh Surface Water Dynamics Analysis (GEE)

A scientifically rigorous Google Earth Engine (GEE) framework designed to quantify surface water extent, flood dynamics, and water body transitions across the Bangladesh Delta. This codebase improves upon standard remote sensing scripts by addressing specific hydrological challenges unique to monsoon-driven deltaic environments.
🚀 Key Achievements & Scientific Improvements

This repository implements a "Publication-Grade" workflow that fixes common errors found in standard Landsat water detection scripts:

    Robust Area Calculation: Replaced fragile band-dependent reducers with a binary pixel-area calculator that eliminates null/zero statistic errors.

    Monsoon Physics: Explicitly separates Monsoon (Jun-Sep) and Dry (Nov-Feb) seasons to capture true hydrological extremes rather than annual averages.

    Flood Memory: Uses 75th Percentile Compositing (instead of the median) to retain episodic floodwater extent often smoothed out by standard reducers.

    SLC-Off Correction: Automatically handles Landsat 7 Scan Line Corrector (SLC) failures (2003–2013) by merging data or falling back to Landsat 5 TM.

    Mangrove Suppression: Implements NDVI thresholds to prevent dark, wet mangrove forests (Sundarbans) from being falsely classified as open water.

    Coastal Guarding: Strict clipping to the FAO GAUL boundary prevents the Bay of Bengal from inflating surface water statistics.

📊 Datasets & Methods
Component	Dataset / Method	Details
Long-Term Baseline	JRC Global Surface Water v1.4	Used for "Lost" vs "Permanent" water stats (1984–2021).
Seasonal Dynamics	Landsat 5, 7, 8, 9 (Level 2)	Cloud-masked, harmonized time series (1990–2024).
Water Index	MNDWI + NDVI Filter	Modified Normalized Difference Water Index with veg suppression.
Cloud Masking	QA_PIXEL Bitmask	C2 Level-2 compliant masking (bits 0-4).
🛠️ Requirements & Usage
Prerequisites

    A valid Google Earth Engine account.

    Access to the GEE Code Editor.

Running the Analysis

    Copy the code from water_analysis.js (or the main script file).

    Paste it into the GEE Code Editor.

    Important: If using the Machine Learning (ML) module, replace the dummy training points in createStratifiedTrainingData() with real geometries using the map tools.

    Click Run.

    View the charts in the Console and export GeoTIFFs via the Tasks tab.

⚠️ Scientific Limitations

    Cloud Cover Bias: During extreme monsoon years (e.g., 1998), cloud cover in Bangladesh can exceed 90% for months. While this script uses a relaxed threshold (80%) and pixel-based masking, some seasonal composites may still have data gaps.

    Resolution: Analysis is performed at 30m (Landsat scale). Small ponds (<900m²) common in rural Bangladesh may be omitted.

    Machine Learning: The included Random Forest classifier is for demonstration. For publication usage, users must generate their own stratified training dataset (50+ points per class).

📄 Outputs

The script generates:

    Statistical Report: Console printout of Permanent, Seasonal, and Lost water area (km²).

    Time Series Charts: Monsoon vs. Dry season water extent trends (1990–2023).

    GeoTIFF Exports: High-resolution rasters for "Lost Water" and "Water Occurrence".
