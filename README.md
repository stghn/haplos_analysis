# haplotype Analysis   
For haplotype analysis, The  R scripts developed to import haploview output and phased data (beagle v3)  
The outputs from these R scripts are:  
  - Extracting haplotypes with a haplo-block and converting into either **genotype counts (0,1,2)** or **plink - ped+map format**  
  - Computing **genomic relationship with the haplotypes** (coded as genotype counts) using vanRaden method 1 or 2  
  **haplo-block** ==> *n* markers make a block  
  **haplotypes**  ==> the haplotypes within a block - (maximum number of haplotypes is **twice the number of samples**)  

## R-scripts  

A) *haplotypeBLgenogrm.R* script - contains four main R-functions:  
    - **getblockhaploview**(haploviewfile)  
    - **makehaplotypes**(phasedbgl, mapinfohap, hapblocks)  
    - **hapgenomatrix**(HAP_ALLELES, HAP_FREQ, MAP_info, hapfreqThresh=0.05, outname)   
    - **hapGRM**(haplomatrix, outputType, method='vanRaden1', outname)  
    
B) *runexample_haplos.R* script - running the example dataset 

The example dataset contains:  
1) example_haplo.ped + example_haplo.map + example_haplo.pheno - **(Plink --ped + --map + --pheno files)**   
2) example_haplo.info - **haploview info file**  
3) example_haplo.blocks - **output of haploview (haplo-blocks)**  
4) bgl.phased.gz - **Beagle v3 phased data**  

### How to prepare the external files  
1. haplotypes blocks are created with haploview (using any of the block definition)  
2. haplo-blocks are exported from haploview (use the **'export options'** under the **'File'** tab in haploview)  
3. The whole segement or a longer segment (example whole chromosome) is phased with BEAGLE v3  

### Data requirement to use the R scripts  
1. The exported haplo-blocks (exported from haploview) file  
2. phased data file from BEAGLE v3  
3. marker MAP information (this should be the same order and size as the marker info file used in haploview)   

See the ***"runexample_haplos.R"*** script for running the example file  

## The funtions  
- **getblockhaploview**(haploviewfile)  
    -  **haploviewfile** argument: The output of haploview (haplo-blocks)  

- **makehaplotypes**(phasedbgl, mapinfohap, hapblocks)  
   - **phasedbgl** argument: Beagle v3 phased data  
   - **mapinfohap** argument: Marker MAP information (same order as the genotypes used in the haploview analysis)  
   - **hapblocks** argument: The R-object of haplo-blocks extracted with the 'getblockhaploview' function above  

- **hapgenomatrix**(HAP_ALLELES, HAP_FREQ, MAP_info, hapfreqThresh=0.05, outname)  
    - **HAP_ALLELES**: R-object that specify the haploytpes generated with the 'makehaplotypes' function above  
    - **HAP_FREQ**: R-object that contains the haploytpe frequecies - also generated with 'makehaplotypes' function  
    - **hapfreqThresh**: threshold for haplotypes in a block  
    - **outname**: output name as plink ped+map files will be generated  

- **hapGRM**(haplomatrix, outputType, method='vanRaden1', outname)  
    - **haplomatrix** argument: R-object that specify the haploytpes generated with the 'hapgenomatrix' function above  
    - **outputType** argument: The output should be a full-matrix [use -'matrix'] or row and column wise [use-'rowcolwise']  
    - **method** argument: vanRaden (2008) method 1 (ZZ'/sum(2pq)) [use - 'vanRaden1'] or method 2 (ZDZ'/Nsnps) [use - 'vanRaden2']  
    - **outname** argument: output name for the grm  

