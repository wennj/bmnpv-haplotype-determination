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

| Isolate  | BioSample    | NCBI SRA (Illumina) | NCBI SRA (Nanopore) |
|----------|--------------|---------------------|---------------------|
| BmNPV-My | SAMN18849911 | SRR14313723         | SRR26992684         |
| BmNPV-Ja | SAMN18849913 | SRR14313721         | SRR26992682         |

## Detailed R code of the workflow

The here presented workflow is conducted under R programming language. Therefore, make sure that [R](https://a-little-book-of-r-for-bioinformatics.readthedocs.io/en/latest/src/installr.html) is installed and working.

[A detailed script written as an R Markdown document can be found here.](/haplotype_workflow.Rmd)

------------------------------------------------------------------------

## Part 1: Determination of variable single nucleotide variants (SNV) using Illumina sequencing data

Dieser Abschnitt bedient sich einem Standardverfahren zur Bestimmung von variablen SNV Positionen. Di

\<tbd\>
