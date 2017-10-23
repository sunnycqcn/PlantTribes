# PlantTribes
## Overview
PlantTribes is a collection of automated modular analysis pipelines that utilize objective classifications of complete protein sequences from sequenced plant genomes to perform comparative evolutionary studies. It post-processes *de novo* assembly transcripts into putative coding sequences and their corresponding amino acid translations, locally assembles targeted gene families, estimates paralogous/orthologous pairwise synonymous/non-synonymous substitution rates for a set of gene sequences, classifies gene sequences into pre-computed orthologous plant gene family clusters, and builds gene family multiple sequence alignments and their corresponding phylogenies. 

Please submit all questions, inquires, and bugs using the PlantTribes repository [issues](https://github.com/dePamphilis/PlantTribes/issues) tab.

In addition to this README file, you can consult the PlantTribes [manual](docs/PlantTribes.md) for more detailed information.

## Installation
PlantTribes pipeline scripts have many external dependencies that need to be installed and available on the environment's $PATH before the pipelines can be used.
#### Pipelines dependencies
- **AssemblyPostProcessor pipeline**:  
[ESTScan (version 2.1)](http://estscan.sourceforge.net/), [TransDecoder (version 3.0.1)](https://github.com/TransDecoder/TransDecoder/releases), [HMMSearch (HMMER version 3.1b1)](http://hmmer.janelia.org/),  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/), and [GenomeTools (version 1.5.4)](http://genometools.org/).
- **GeneFamilyClassifier pipeline**:  
[BLASTP (NCBI BLAST version 2.2.29+)](http://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download), and [HMMScan (HMMER version 3.1b1)](http://hmmer.janelia.org/).
- **PhylogenomicsAnalysis pipeline (legacy pipeline)**:  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PASTA](https://github.com/smirarab/pasta), [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/), [RAxML (version 8.1.16)](http://sco.h-its.org/exelixis/web/software/raxml/index.html),  
and [FastTreeMP (version 2.1.7 SSE3)](http://meta.microbesonline.org/fasttree/).
- **GeneFamilyIntegrator**:  
No external dependencies required.
- **GeneFamilyAligner pipeline**:  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PASTA](https://github.com/smirarab/pasta), and [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/).
- **GeneFamilyPhylogenyBuilder pipeline**:  
[RAxML (version 8.1.16)](http://sco.h-its.org/exelixis/web/software/raxml/index.html), and [FastTreeMP (version 2.1.7 SSE3)](http://meta.microbesonline.org/fasttree/).
- **KaKsAnalysis pipeline**:   
[MAKEBLASTDB/BLASTN (NCBI BLAST version 2.2.29+)](http://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download), [CRB-BLAST (version 0.6.9)](https://github.com/cboursnell/crb-blast), [MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PAML (version 4.8)](http://abacus.gene.ucl.ac.uk/software/paml.html#download),  
and [EMMIX (version 1.3)](https://people.smp.uq.edu.au/GeoffMcLachlan/emmix/emmix.html).

#### PlantTribes scaffolds data 
- **22 plant genomes (Angiosperms clusters, version 1.0)**  
Download: http://fgp.huck.psu.edu/planttribes_data/22Gv1.0.tar.bz2  
<!--- MD5 checksum: `4f09c41683d1ea0670b38cef640fb548` --->  
- **22 plant genomes (Angiosperms clusters, version 1.1)**  
Download: http://fgp.huck.psu.edu/planttribes_data/22Gv1.1.tar.bz2  
<!--- MD5 checksum: `0025188cdeccfb828fbebabb923963bd` --->

#### Install PlantTribes
1. Open a terminal and change to the location where you would to keep PlantTribes. 
  - Example: `cd ~/softwares`
2. Clone the [PlantTribes](https://github.com/dePamphilis/PlantTribes) GitHub repository or download the [zip archive](https://github.com/dePamphilis/PlantTribes/archive/master.zip) and decompress it in your desired location.   
  - Examples: `git clone https://github.com/dePamphilis/PlantTribes.git` or `unzip https://github.com/dePamphilis/PlantTribes/archive/master.zip`
3. Download the scaffold data set(s) that you would like to use into the PlantTribes' [data](data) subdirectory and decompress them.
  - Examples: `cd PlantTribes/data`, `md5sum 22Gv1.1.tar.bz` (should match the provided MD5 checksum for the data archive), followed by `tar -xjvf 22Gv1.1.tar.bz2`

## Using PlantTribes
The execulables for the PlantTribes pipelines are in the [pipelines](pipelines) subdrectory of the installation. You can either add them to your PATH environment variable or execute directly from the PlantTribes installation.

- **AssemblyPostProcessor pipeline**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/AssemblyPostProcesser`
  - Basic run using ESTScan prediction method:
    - `PlantTribes/pipelines/AssemblyPostProcesser  --transcripts transcripts.fasta --prediction_method estscan --score_matrices /path/to/score/matrices/Arabidopsis_thaliana.smat`
- **GeneFamilyClassifier pipeline**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyClassifier`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and blastp classifier:
    - `PlantTribes/pipelines/GeneFamilyClassifier --proteins proteins.fasta --scaffold 22Gv1.1 --method orthomcl --classifier blastp`
- **PhylogenomicsAnalysis pipeline**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/PhylogenomicsAnalysis`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and raxml Phylogenetic trees inference method:
    - `PlantTribes/pipelines/PhylogenomicsAnalysis --orthogroup_faa geneFamilyClassification_dir/orthogroups_fasta --scaffold 22Gv1.1  --method orthomcl  --add_alignments  --tree_inference raxml`
- **GeneFamilyIntegrator**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyIntegrator`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method:
    - `GeneFamilyIntegrator --orthogroup_faa geneFamilyClassification_dir/orthogroups_fasta --scaffold 22Gv1.1  --method orthomcl`
- **GeneFamilyAligner pipeline**:  
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyAligner`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and mafft alignment method:
    - `GeneFamilyAligner --orthogroup_faa integratedGeneFamilies_dir --alignment_method mafft`
- **GeneFamilyPhylogenyBuilder pipeline**:  
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyPhylogenyBuilder`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and fastree Phylogenetic trees inference method:
    - `GeneFamilyPhylogenyBuilder --orthogroup_aln geneFamilyAlignments_dir/orthogroups_aln --tree_inference fasttree`     
- **KaKsAnalysis pipeline**
  - Display all usage options:
    - `PlantTribes/pipelines/KaKsAnalysis`
  - Basic run using for paralogous analysis:
    - `KaKsAnalysis --coding_sequences_species_1 species1.fna --proteins_species_1 species1.faa --comparison paralogs --num_threads 4`

Please consult the PlantTribes [manual](docs/PlantTribes.md) and [tutorial](docs/Tutorial.md) for a detailed description and usage of all options for the pipelines respectively.

## License
PlantTribes is distributed under the GNU GPL v3. For more information, see [license](LICENSE).
