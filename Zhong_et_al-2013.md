# BCB 546 Final Project
Ludvin Mejia and David Hall

## Genetic Analysis of Invasive *Aedes albopictus* Populations in Los Angeles County, California and Its Potential Public Health Impact
- [Link to Article](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3702605/)

### Background
*Aedes albopictus* is one of the most invasive insects in the world. Factors including globalization and climate change have driven the spread from its native home in SE Asia to every continent except Antarctica in 30-40 years. As an efficient vector for viruses like dengue, Zika, and Chikungunya, the spread of this species of mosquito can be a significant threat to public health. While *Aedes albopictus* was introduced to the U.S. in Louisiana or Texas around 1985, a significant introduction did not occur in California until 2001. It is believed that this introduction was due to a shipment of lucky bamboo from China, and aggressive control efforts were undertaken to try and eliminate this population. While control efforts were believed to be a success, another population of *Aedes albopictus* was detected in Los Angeles in 2011. The goal of this study is to try to determine the origin of this 2011 population, and to determine whether this population is a carryover from the introduction in 2001, or represents a new introduction entirely.

To answer this question, they extracted DNA from 346 *Aedes albopictus* mosquitoes from around the world, including samples from the Los Angeles introductions in 2001 and 2011. They then sequenced a portion of the mitochondrial CO1 gene for each sample, and analyzed the genetic relationships between these samples.

### Analysis to be reproduced

We chose to attempt to recreate [figure 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3702605/figure/pone-0068586-g001/) from this study. 
- A phylogenetic network of the 66 haplotypes these researchers detected
- Shows close relationship of haplotypes collected in Los Angeles in 2001 and 2011 to haplotypes detected in southern China and Singapore
- Shows samples collected from Texas, New Jersey, and Italy are closely related, but distantly related to Los Angeles samples
- Supports temperate Asian origin for LA samples

## Our Analysis

### Sequence Data and alignment verification

- 66 representative sequences downloaded from [GenBank](https://www.ncbi.nlm.nih.gov/nuccore/KC690896,KC690897,KC690898,KC690899,KC690900,KC690901,KC690902,KC690903,KC690904,KC690905,KC690906,KC690907,KC690908,KC690909,KC690910,KC690911,KC690912,KC690913,KC690914,KC690915,KC690916,KC690917,KC690918,KC690919,KC690920,KC690921,KC690922,KC690923,KC690924,KC690925,KC690926,KC690927,KC690928,KC690929,KC690930,KC690931,KC690932,KC690933,KC690934,KC690935,KC690936,KC690937,KC690938,KC690939,KC690940,KC690941,KC690942,KC690943,KC690944,KC690945,KC690946,KC690947,KC690948,KC690949,KC690950,KC690951,KC690952,KC690953,KC690954,KC690955,KC690956,KC690957,KC690958,KC690959,KC690960,KC690961) in FASTA format using accession numbers provided in the supplement
  - `Haplotypes.fasta` alignment can be found in the DATA folder of the repository
- Alignment of sequences verified by inspection in [BioEdit v 7.0.5.3](https://bioedit.software.informer.com/7.0/)
  - The authors aligned and edited their sequences manually using bioedit (raw data is not available)
  - While the sequences that are available are effectively already aligned (all the same length, positions in the C01 gene), we decided to also align and inspect them in python, which would have been a more robust method originally
  - Inspection using [Bio.AlignIO](https://biopython.org/docs/1.76/api/Bio.AlignIO.html) and `Alignment.ipynb` script found in the software folder of the github repository.

### Identifying sequence polymorphisms

- The `Haplotypes.fasta` alignment file was opened using [DnaSP v6.12.03](http://www.ub.edu/dnasp/)
- From the DnaSP menu, we selected Generate --> Polymorphic/Variable Sites Data File...
  - Options: 
    - Included all 66 sequences
    - From site 1 to 1433
    - Sites with alignment gaps excluded
    - All substitutions are considered
- This generated a file containing sequence polymorphism data in nexus format we named `polymorphic_sites.nex`
  - `polymorphic_sites.nex`is available in the github repository under the data folder

### Adding location data

- Location data where the samples were collected was provided by the authors in the supplement
  - This data is contained in `Zhong_et_al_haplotypes.csv` in the data folder of the github repository
  - `Zhong_et_al_haplotypes.csv` also contains their sequence polymorphism data, so we extracted the location data to a new file called `locations.csv`
- We wrote a Python script to extract location data from `locations.csv` and append it to `polymorphic_sites.nex`, creating `polymorphic_sites_locations.nex`
  - This Python script can be found as `Location_data.ipynb` in the software folder of the github repository
  - This script converts location data to a format readable by PopART for the next step
  - This script also converts GenBank accession numbers to the haplotype numbers used by Zhong et al. for readability and visualization

### Creating the haplotype network

- We could not access [TCS](https://onlinelibrary.wiley.com/doi/full/10.1046/j.1365-294x.2000.01020.x?sid=nlm%3Apubmed), the original software used to create the haplotype network as the link in this source appears to be broken.
  - There is [another paper](https://academic.oup.com/jme/article/57/5/1488/5804183?login=true) that cites Zhong et al and performs a similar analysis
  - We used the software used in this paper to perform our analysis
- `plymorphic_sites_locations.nex` was opened in [PopART v1.7](https://popart.maths.otago.ac.nz/)
  - From the PopART menu we selected Network --> TCS Network
  - Colors were edited to match RGB values from the original figure using Edit --> Set Trait Color
  - Nodes and labels were rearranged for clearer visualization
- Final PopART file can be found as `polymorphic_sites_loctations_popart.nex` in the Data folder of the GitHub repository
- Final image produced can be found as `haplotype_network` in the presentation folder of the GitHub Repository

## Comparison and Challenges

### Comparison

- Our results are generally similar to Zhong et al., and support some of the same conclusions:
  - New Jersey (NJ), Texas (TX), and Italy (IT) populations are closely related
  - "Group 1" is largely preserved in our analysis
  - LA01 and LA11 populations are most closely related to populations from southern China (GZ,XM,JS) and Singapore (SG)

- There are some minor differences in our results:
  - individual connections appear to be variable, even if the trend is the same
  - "Group 2" and "group 3" are not as apparent in our analysis
  - Seem to be some minor differences in the smaller haplotypes

- There are also some major differences:
  - H17 does not appear in the Zhong et al network
  - H17 appears to be connected to many nodes, and is one of the most connected haplotypes in our analysis
  - After double checking, we believe this is not our mistake, and is present in the data provided
  - While it does not appear to alter conclusions, it may have an impact on down stream results that we did not replicate

### Challenges

- No repository, code, or detailed description of analysis performed made this reproduction a challenge, even with a manageable amount of sequence data
- Without access to raw data, we cannot fully recreate their analysis. For example, we cannot cross check the location data provided with sequence data to determine if there is a mistake (i.e. a typo) regarding H17
- Haplotypes are not labeled in Zhong et al. figure, making direct comparison between the smaller nodes difficult/impossible
