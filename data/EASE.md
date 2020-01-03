# EASE results as a gold-standard results for demixing calcium imaging data

EASE extracts individual neurons from calcium imaging (CI) data by combining dense reconstruction of electron microscopy (EM) data. Thus each extracted components has an EM match, which provides the ground truth of the neuron's ROI. Hence we relase the EASE results a 'gold standard' to score and optimize the pipelines for demixing two-photon CI data. 

**Notes**

* The data and results in this folder will be updated continuously as we process more data and refine our analysis. 
* We are not 100% sure of the match between the extracted 2P neuron and EM neuron. There is a confidence score to quantify our matching confidences. The larger, the better. 
* when you use the data, you need to cite the paper xxx. 


**data description** 

We currently only release 1 dataset 
* pinky40: 4 scans; simultaneously recorded 3 planes in one scan; frame rate 14.8313 Hz; 


Here is how the data were organized for each dataset. 

* each dataset has a separate folder. 
* the CI data are saved into a subfolder of each dataset folder. The files are named in the format of 'scan**x**_block**y**_complete.mat', where **x** is the scan ID and **y** is the block ID. Blocks are temporally divided videos and they have the same spatial FOV for one scan. 
* each 'scan**x**_block**y**_complete.mat' file has a d1 x d2 x d3 x T high-dimension array. That's the video data for this specific scan and specific block. 
* The EASE results were saved into the subfolder 'results' of each dataset folder. They were named in the format like **results_v1_20190512.mat**, where v1 is the version number and 20190512 specifies the date. 
* within each result file, there is a struct variable storing the results of all scans. It has following fields that you might be interested in: 
  * dims: a vector [d1, d2, d3, scan_numbers] 
  * EM_voxels: a cell array; each element is a d1 x d2 x d3 boolean array, which specifies the voxels that are within the EM volume.  
  * A: d x K matrix; spatial footprints of the K extracted neurons from CI data in all scans. d = d1 x d2 x d3 x scan_numbers. 
  * A_em: d X K matrix. same as A, except that these components are created by downsampling the meshes of the matched EM components. 
  * Craw: T * scan_numbers *  K ndarray; The raw temporal traces of each neuron in each scan; We usually combine all blocks into one and ignore the first 200 frames because these frames are blank. This applies to C and S too. 
  * C: T * scan_numbers *  K ndarray; The denoised temporal traces of each neuron in each scan; 
  * S: T * scan_numbers *  K ndarray; The deconvolved temporal traces of each neuron in each scan; 
  * confidences: scan_numbers X K matrix; the confidence score of matching the extracted neuron to the corresponding EM component. 
  * detected: scan_numbers X K boolean matrix; the indicator of whether a neuron is detected in that scan. If it's zero, then the related A and C will be 0. 

You can send an email to zhoupc2018@gmail.com for more information relating to the results. 