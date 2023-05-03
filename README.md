# BCB 546 Final Project

## Data

### `Haplotypes.fasta`
A FASTA file containing 66 representative haplotype sequences provided by Zhong et al. and downloaded directly from GenBank 

### `Zhong_et_al_haplotypes.csv`
Supplement file provided by Zhong et al. containing a summary of the locations where samples were collected and breakdown of polymorphic sites

### `locations.csv`
Location data copied directly from `Zhong_et_al_haplotypes.csv`

### `polymorphic_sites.nex`
Ouput nexus file conataining polymorphic sites from DNAsp v6.12.03 using Haplotypes.fasta as input

### `polymorphic_sites_locations.nex`
polymorphic sites data from `polymorphic_sites.nex` with location data from `locations.csv` appended in nexus format using `location_data.ipynb`
For simplicity, GenBank accession numbers are also replaced with haplotype numbers used by Zhong et al. 

## Software

### `location_data.ipynb`
jupyter notebook containing commented python script used to append location data from `locations.csv` to `polymorphic_sites.nex`
Also containes find and replace script that replaces GenBank accession numbers with haplotype numbers used by Zhong et al.

### `Alignment.ipynb`
jupyter notebook containing python script used to verify and inspect alignment of `Haplotypes.fasta`