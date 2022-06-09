# radiomics-for-srs-performance-sensitivity-data-share
Open-source sample labels, groupings and positive label confidences results associated with the results presented in the manuscript "Brain Metastasis Stereotactic Radiosurgery Outcome Prediction using MRI Radiomics: Performance Sensitivity to Primary Cancer, Metastasis Volume and Scanner Type"

## Data Description

### Root Directory
**Sample Groupings and Ground Truth Labels.xlsx** - Provides a list of the patient and brain metastasis ID for each brain metastasis (sample) in the study (n=123). Samples are uniquely identified using the patient ID and metastasis ID pair. For each sample, the ground truth label is provided. If the value is "1", the sample is positive, meaning that the brain metastasis progressed post-SRS. Otherwise the sample is negative. For each sample, the primary cancer site (for the associated patient), metastasis volume and MRI scanner model used for acquiring the pre-treatment imaging is provided. This allows for each sample to be categorized into the specific primary cancer site, volume and MRI scanner model sub-populations analyzed.

### Clinical and Radiomic Features Predictive Accuracy
**Clinical Features Only (Testing Datasets Results).xlsx** - Each sheet in file provides the positive label confidence for each sample in the testing dataset for each bootstrap resampling iteration. Each iteration is cataloged in its own sheet labeled as "Iter. XXX". The positive label confidence is the confidence the iteration's trained random decision forest provided as output when the testing data set sample in question was provided as input. A value of "0" indicates the model being the most confident the sample is negative; "1" indicates the model being the most confident the sample is positive. Due to the random bootstrap resampling during each iteration and its application on a per patient basis, the number of samples in each testing set varies between iterations, but will be approximately (1-0.632) x 123 = 45. The last sheet in this file, "All Samples", refers to a final iteration in which the entire dataset is used in training and testing, as required for computation of the AUC_0.632+ error metric. This is why all 123 samples are present in this sheet. 

In comparison to the other "Testing Datasets Results" files in the directory, this file contains only the results produced when using solely clinical features and no radiomic features.

**Clinical Features Only (OOB Datasets Results).xlsx** - See the description above for *Clinical Features Only (Testing Datasets Results).xlsx* on the structure of the file. In contrast to *Clinical Features Only (Testing Datasets Results).xlsx*, this file contains the positive label confidences produced by the out-of-bag (OOB) samples of the training dataset for each bootstrap resampling iteration. Given the random bootstrap resampling during each iteration, the number and order of the samples will be random. As bootstrap resampling is done with replacement, the same sample may appear multiple times in the training dataset for the same iteration. The number of samples for each iteration will be roughly 123, but will vary slightly due to samples being included per patient. The number of unique samples for each iteration will be approximately 0.632 x 123 = 78. As the OOB samples are also randomly selected from the training dataset for each tree in the random forest, the positive label confidence for the same repeated sample within one iteration may differ.

In comparison to the other "OOB Datasets Results" files in the directory, this file contains only the results produced when using solely clinical features and no radiomic features.

**Radiomic Features Only (Testing Datasets Results).xlsx** - Provides the testing dataset positive label confidence values produced when using solely radiomic features and no clinical features. See the description for *Clinical Features Only (Testing Datasets Results).xlsx* for details on the file structure.

**Radiomic Features Only (OOB Datasets Results).xlsx** - Provides the out-of-bag dataset positive label confidence values produced when using solely radiomic features and no clinical features. See the description for *Clinical Features Only (OOB Datasets Results).xlsx* for details on the file structure.

**Clinical & Radiomic Features (Testing Datasets Results).xlsx** - Provides the testing dataset positive label confidence values produced when using clinical and radiomic features. See the description for *Clinical and Radiomic Features (Testing Datasets Results).xlsx* for details on the file structure.

**Clinical & Features (OOB Datasets Results).xlsx** - Provides the out-of-bag dataset positive label confidence values produced when using clinical and radiomic features. See the description for *Clinical and Radiomic Features  (OOB Datasets Results).xlsx* for details on the file structure.

### Volume Dependency of Predictive Accuracy

See the description under the *Clinical and Radiomic Features Predictive Accuracy* heading for details on file structure and the difference between "Testing Datasets Results" and "OOB Datasets Results" files.

The positive label confidence results for each correlation cut-off (0, 0.1, 0.25, 0.4, 0.55, 0.7, 0.85, 1) are provided in the correspondingly named files. **Note:** The files for correlation cut-off = 1 are identical to those for clinical and radiomic features in the *Clinical and Radiomic Features Predictive Accuracy* directory, as a cut-off of 1 signifies the removal of no features.

### Effects of Multiple MR Scanner Models

See the description under the *Clinical and Radiomic Features Predictive Accuracy* heading for details on file structure and the difference between "Testing Datasets Results" and "OOB Datasets Results" files.

The positive label confidence results for each scanner pairing (Vision & Expert, Vision & Avanto, Expert & Avanto) are provided in the correspondingly named files.


## Data Usage

With the data shared within this repository, a user would be able to reproduce the full error metric analysis presented in the accompanying manuscript.

The results presented in the *Clinical and Radiomic Features Predictive Accuracy* section of the paper could be replicated using the ground truth labels contained within *Sample Groupings and Ground Truth Labels.xlsx* along with the positive label confidences within the *Clinical and Radiomic Features Predictive Accuracy* directory's files. The positive label confidences and ground truths labels for the OOB datasets across bootstraps could be used to construct an average receiver operating characteristic (ROC) curve based on the training datasets and choose an optimal operating point. The positive label confidences and ground truths labels for the testing datasets across bootstraps could be used to construct an average ROC curve based on the testing datasets. The area-under-the-ROC-curve (AUC) could be found directly from this ROC curve, and the misclassification rate, false negative rate, and false positive rate could be found using the optimal operating point found using the OOB datasets previously. The positive label confidences and ground truths labels for the testing datasets could also be used to calculate the corrected AUC_0.632+ value. This analysis could be repeated for using clinical features only, radiomic features only, and clinical and radiomic features together to fully reproduce all of the results presented in the paper section.

The results presented in the *Primary Cancer Site Dependency of Predictive Accuracy* section of the paper could be replicated following the process described above for *Clinical and Radiomic Features Predictive Accuracy*, except that the primary cancer site per sample data contained within *Sample Groupings and Ground Truth Labels.xlsx* would have to first be used to properly stratify the samples.

The results presented in the *Volume Dependency of Predictive Accuracy* section of the paper could be replicated following the process described above for *Clinical and Radiomic Features Predictive Accuracy*, except that the positive label confidences provided per correlation cut-off in the *Volume Dependency of Predictive Accuracy* directory would be used. The same error metric analysis is repeated for each correlation cut-off value to achieve the error metrics across all samples, whereas error metric calculation per volume group is achieved via stratification of samples into volume groups using the volume data in *Sample Groupings and Ground Truth Labels.xlsx*.

Lastly, the results presented in the *Effects of Multiple MR Scanner Models* section of the paper could be replicated following the process described above for *Clinical and Radiomic Features Predictive Accuracy*, except that error metrics would be found for each of the three MR scanner model pairings, instead of for using clincial and/or radiomic features.


## Contact Information
Author: David A. DeVries

Email: ddevrie8@uwo.ca

Organization: Western University/London Health Sciences Centre, London ON CA