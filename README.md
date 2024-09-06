# EPICV2 Deconvolution

This code is an adaptation of @nloyfer's methylation atlas [deconvolution scripts ](https://github.com/nloyfer/meth_atlas?tab=readme-ov-file) that have been changed to work with EPICV2 data. These scripts run the deconvolution method developed by [Moss et al. 2018](https://www.nature.com/articles/s41467-018-07466-6).

**For processing the array data:**
 - reassign_minfi_funcs_EpicV2.R reassigns two minfi functions (.isEpic and combineArrays) to detect EpicV2 array data, and to load the appropriate annotation
 - process_array_kitzhu2.R is adapted from @nloyfer's process_array.R. It has been changed to:
      1.  Run reassign_minfi_funcs_EpicV2.R after loading in minfi
      2.  Only load in the group of samples that are derived from whole blood.
      3.  Exclude the use of a reference sample (since the whole blood samples are being processed and normalized as a group, a ref sample is no longer necessary).
  
 - To run: `Rscript process_array_kitzhu2.R ./idats/ ./Blood_Decon_LoyferMethod.csv`

**For generating the deconvolution estimates:**
- reference_atlas_EpicV2.csv is an updated reference atlas that has EPICV2 probe IDs (these are matched by underlying sequence to the original EPICV1 probe IDs)
- The updated reference atlas includes a total of 5620 probes that are retained from the original 6105 V1 probes in the reference atlas. This equals a 92% retention rate, which is actually higher than the total number of probes retained between the arrays (83%). I still have to do some testing to make sure this doesnt significantly impact performance.

- To run: `deconvolve.py -a reference_atlas_EpicV2.csv Blood_Decon_LoyferMethod.csv`
