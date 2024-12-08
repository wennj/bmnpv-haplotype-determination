# A workflow for linking Nanopore reads using single nucleotide variants (SNV) to reconstruct genomic haplotypes

The figures and content in this repository are derived from the following publication:

**Wennmann, J.T., Lim, F.S., Senger, S., Gani, M., Jehle, J.A., Keilwagen, J (2024). Haplotype determination of the Bombyx mori nucleopolyhedrovirus by Nanopore sequencing and linkage of single nucleotide variants.** Journal of General Virology. 105 (5), 001983. [<https://doi.org/10.1099/jgv.0.001983>]

------------------------------------------------------------------------

## Challenges in deciphering virus populations by sequencing

Virus isolates can contain many different haplotypes, which can have different biological properties. For genome sequencing, genomic DNA is extracted, fragmented and then sequenced. The sequence fragments must then be assembled into a consensus sequence using bioinformatic tools. However, a consensus sequence usually represents a majority and can hide genetic intra-isolate diversity. There are many different bioinformatic tools and workflows available to perform haplotype-sensitive assemblies. But usually these workflows are established for viruses with relatively short genomes. For viruses with large genomes, this is not yet possible.

*How can we achieve a haplotype-sensitive assembly to reveal intra-isolate variability*? This question concerns all nuclear arthropod large DNA viruses (class Naldaviricetes), as especially many genome are being sequenced here (see image below).

![](https://github.com/wennj/naldv-whole-genome-reads/blob/main/output/ncbi_stats/NALDV_stats_on_Genbank_SRA.png)

## Aim of this repository

This repository aims to demonstrate the workflow for determining the haplotypes of a population of baculoviruses using Illumina and Nanopore data sets. The prerequisite is that both sequencing data sets originate from the same DNA. At first, the variable SNV positions are determined from the Illumina data, as these have a very low probability of error, using a reference genome. The obtained information on the on the SNV positions is then transferred to the Nanopore reads, as these are considerably longer and can include several SNV positions. Due to the read's length, SNV linkage allows the assignment of the Nanopore reads to components, for which machine learning is used. All these steps should show how sequence data can be divided into components that represent main haplotypes.

## Further reading

Even though the below presented workflow should be easy to understand and follow, I would still like to point out that the method is based on and inspired by the following publications and their corresponding Github repositories:

-   Gani et al. (2021). Patterns in Genotype Composition of Indian Isolates of the Bombyx mori Nucleopolyhedrovirus and Bombyx mori Bidensovirus. Viruses. 13(5):901. [<https://doi.org/10.3390/v13050901>]

-   Fan et al. (2020). Population structure of Cydia pomonella granulovirus isolates revealed by quantitative analysis of genetic variation. Virus Evolution. 7(1):veaa073. [<https://doi.org/10.1093/ve/veaa073>]

-   Wennmann et al. (2020). Bacsnp: Using single nucleotide polymorphism (SNP) specificities and frequencies to identify genotype composition in baculoviruses. 12(6):625. [<https://doi.org/10.3390/v12060625>] [<https://github.com/wennj/bacsnp>]

------------------------------------------------------------------------

## Example data and bioinformatic platform(s)

The data sets used in this exemplary workflow are freely available under [NCBI BioProject PRJNA724724](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA724724) ‘*Isolates of the Bombyx mori nucleopolyhedrovirus from India*’. Here, the data sets of two isolates of Bombyx mori nucleopolyhedrovirus (BmNPV) can be downloaded and processed. For bioinformatic analysis of the data, I recommend a Galaxy platform for less experienced and beginners: [usegalax.eu](https://usegalaxy.eu/) or [nanopore.usegalaxy.eu](https://nanopore.usegalaxy.eu/). Any other Galaxy platform is also suitable, of course. An experienced bioinformatician can carry out all analyses using the command line on her or his system of choice.

Here are the NCBI sequence read archive (SRA) data sets that are used in this workflow:

| Isolate  |  BioSample   | NCBI SRA (Illumina) | NCBI SRA (Nanopore) |
|:--------:|:------------:|:-------------------:|:-------------------:|
| BmNPV-My | SAMN18849911 |     SRR14313723     |     SRR26992684     |
| BmNPV-Ja | SAMN18849913 |     SRR14313721     |     SRR26992682     |

Für die SNV Bestimmungen wird eine Referenz benötigt. Diese muss nah mit den sequenzierten Isolaten verwandt sein. Da es sich bei den Proben um Isolate des BmNPV handelt, die aus Indien stammen, eignet sich die Genomsequenz des BmNPV-India:

| Name | GenBank Accession no. | Length (bp) | GC (%) | Pubmed ID |
|:--:|:--:|:--:|:--:|:--:|
| BmNPV-India | [JQ991010](https://www.ncbi.nlm.nih.gov/nuccore/JQ991010.1) | 126879 | 40.4 | [23043173](https://pubmed.ncbi.nlm.nih.gov/23043173/) |

## Detailed R code of the workflow

The here presented workflow is conducted under R programming language. Therefore, make sure that [R](https://a-little-book-of-r-for-bioinformatics.readthedocs.io/en/latest/src/installr.html) is installed and working.

[A detailed script written as an R Markdown document can be found here.](/haplotype_workflow.Rmd)

------------------------------------------------------------------------

## Part 1: Determination of variable single nucleotide variants (SNV) using Illumina sequencing data

In this section a standard method for determining variable SNV positions is demonstrated. There are many methods for variable SNP position determination, but the here method presented has been proven to work well for sequenced isolates of baculoviruses. It was further used for the bacsnp tool, which can be used to determin specificities of variable SNV position. The entire workflow to determine variable SNV positions

for sequenced baculoviruses and was also used for the bacsnp tool [<https://doi.org/10.3390/v12060625>] [<https://github.com/wennj/bacsnp>], which determines the specificity of SNV positions. The workflow for determining SNV includes the following tools:

-   Trim Galore! ([Link](https://github.com/FelixKrueger/TrimGalore))

-   BWA-MEM ([Link](https://github.com/galaxyproject/tools-iuc/tree/main/tools/bwa))

-   mpileup ([Link](https://github.com/galaxyproject/tools-iuc/tree/main/tools/bcftools))

-   bcftools ([Link](https://github.com/galaxyproject/tools-iuc/tree/main/tools/bcftools))

A pre-prepared workflow for usegalaxy.eu can be downloaded here [[Link to Galaxy workflow file](https://github.com/wennj/bacsnp/blob/master/doc/Galaxy-Workflow-bacsnp_SNP_calling_workflow.ga)] or viewed directly on usegalaxy.eu [[Link workflow on usegalaxy.eu](https://usegalaxy.eu/published/workflow?id=6223333100a9e73f)].

Below is an overview image of the workflow.

![](https://github.com/wennj/bacsnp/blob/master/assets/galaxy_workflow_screenshot.png)

### Running the workflow

To start the workflow, you should prepare the data as follows:

-   Import the reference (BmNPV-India, JQ991010) into the usegalaxy.eu history in fasta format.

-   Import the SRR files of BmNPV-My (SRR26992684) and BmNPV-Ja (SRR26992681) into the history. Either download the NCBI SRA data sets manually from NCBI SRA and upload them to usegalaxy.eu or use the usegalaxy.eu tool *Faster Download and Extract Reads in FASTQ format from NCBI SRA* (Galaxy Version). The format should be fastq (compressed or uncompressed).

-   Build a list of dataset pairs (Build List of Dataset Pairs) using the downloaded paired datasets of BmNPV-My and BmNPV-Ja.

-   Start the workflow and use the dataset list as read input.. Set the fasta sequence of BmNPV-India as the reference genome.

### Workflow output

\<tbd\>
