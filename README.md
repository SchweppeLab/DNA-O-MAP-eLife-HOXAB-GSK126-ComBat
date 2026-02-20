# DNA-O-MAP HOXA and HOXB ComBat Batch Correction

This repository contains the analysis script and input data for performing batch correction on GSK126-treated and TMT-labeled HOXA and HOXB DNA O-MAP samples.

## Author

**Conor Herlihy**

## Related Publication

This analysis is associated with the "DNA O-MAP uncovers the molecular neighborhoods associated with specific genomic loci" publication in eLife. The DOI for the related paper will be added upon publication.

## Required R Libraries

This script requires the following R packages:

- `tidyverse` - For data manipulation and visualization
- `sva` - For batch effect correction using ComBat

To install these packages in R, run:

```r
install.packages("tidyverse")
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("sva")
```

## Core Functions

The script performs the following key analyses:

1. **Data Loading**: Reads protein quantification data from MS runs of Hox A&B +/-GSK126 samples

2. **Pre-Correction PCA Analysis**: Performs Principal Component Analysis on the raw data to visualize batch effects before correction

3. **ComBat Batch Correction**: Uses the ComBat algorithm from the `sva` package to correct for technical batch effects while preserving biological variation across:
   - HOXA +/- GSK126 treatment
   - HOXB +/- GSK126 treatment
   - Multiple biological replicates (batches 1, 2, 3)
   - Different time points

4. **Post-Correction PCA Analysis**: Re-performs PCA on batch-corrected data to validate the effectiveness of the correction

5. **Data Export**: Outputs the batch-corrected quantification data to a CSV file for downstream analysis

## Usage

The analysis is implemented as an R Markdown document. To run the analysis:

```r
# Open the R Markdown file
# Run all chunks or knit the document
rmarkdown::render("HoxAB_GSK126_ComBat_eLife.Rmd")
```

## Input Data

The script expects a CSV file named `Live_pq_693_TMTMosaic.csv` containing the protein quantification data from theGSK126-treated and TMT-labeled HOXA and HOXB DNA O-MAP experiment.

## Output Files

The script generates the following outputs:

- `HoxAB_GSK126_ComBat_Batch_Corrected.csv` - Batch-corrected quantification data
- `Pre-ComBat_PCA_HoxAB-GSK126.pdf` - PCA plot before batch correction
- `Post_ComBat_PCA_HoxAB-GSK126.pdf` - PCA plot after batch correction (scaled)
- `Unscaled_Post_ComBat_PCA_HoxAB-GSK126.pdf` - PCA plot after batch correction (auto-scaled)

## License

This project is licensed under the MIT License - see the LICENSE file for details.
