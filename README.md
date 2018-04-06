# CSR
Consensus Clustering for Subclonal structure Reconstruction
## Introduction
CSR was originally created for Pan-Cancer Analysis of Whole Genome (PCAWG) working group, Heterogeneity and Evolution, of International Cancer Genome Consortium (ICGC) during the Heterogeneity project. It was used to make a consensus subclonal architecture out of results of 11 participating methods. Please see (Heterogeneity citation) for details.
## Prerequisitions
Part of the calculation depends on SPAMS http://spams-devel.gforge.inria.fr/downloads.html. Please follow the instructions on their website to install spams python3 version (prefer Anaconda distribution).
## Installing
There is no need to install CSR, it runs just like your regular python script.
## Start Your First Example
For your convenience, we supply an example here with 3 methods. https://github.com/kaixiany/CSR/tree/master/Example_input/
### Input format
The input files are tab separated, containing 4 columns: chromosome, position, assignment, CP please see https://github.com/kaixiany/CSR/tree/master/Example_input/sample1/method1Input.tsv for an example.

Please prepare one input file for each method for each sample, and put all input of the same sample in a folder. Please separate samples by folder.

### Preprocess
We supply a preprocess script CSR_preprocess.R to prepare the actual input files for CSR.
```
Rscript CSR_preprocess.R inputDir outputDir DownsampleSize FilteringProp
```
In our example, you can run
```
Rscript CSR_preprocess.R Example_input/sample1/ preprocessed/samples1/ 5000 0.3
```

### Running CSR
After obtained the preprocessed files, you can now run CSR.py by
```
python3 CSR.py path_to_preprocessed path_of_results iteration
```
where iteration can be positive or negative integer. A positive iteration number specifies how many interations should be done when doing matrix decomposition. A negative iteration number specifies the seconds should be run for matrix decomposition. In our example, we can now run
```
python3 CSR.py preprocessed/samples1/ results/sample1/ -30
```
This will write results to results/sample1/, and the matrix decomposition will run for 30 sec.

### Output file
There should be 3 files in the output:

'mutation_assignments.txt': one column text file, each row indicates the cluster id of the mutation

'mutations_list.txt': one column text file, each raw is a position of the mutation in the format 'chr_position'

'summary_table.txt': three columns text file, each row is a cluster. First column is the cluster id, second column is number of SNVs in the cluster， the third column is the cellular prevalence of the cluster.
