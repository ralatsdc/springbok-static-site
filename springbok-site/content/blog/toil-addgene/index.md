+++
title = "Light is the Task where Many Share the Toil"
date = "2022-02-18"
fragment = "content"
weight = 1
important = "true"
subtitle = "Raymond LeClair"

[asset]
image = "toil-image.jpeg"
+++

[*The Bauxite Mines (1942), mural by Julius Woeltz for the U.S. Post Office in Benton, Arkansas*](https://en.wikipedia.org/wiki/File:Mural-Post-Office-Benton-Arkansas.jpg)

*Homer, The Iliad, Book XII, line 493. Bryant's translation.*

___

We are living in what some call a Golden Age of genome engineering. It is now possible for researchers to read DNA sequences, and then directly modify existing DNA sequences to investigate gene function, or create new DNA sequences to synthesize novel biological systems. The technology for these advances have rapidly matured during the last decade. The cost and time required to sequence, or read, genomes has fallen by orders of magnitude, especially due to so-called short-read technologies. Similarly, the time and cost to modify DNA sequences has fallen dramatically, much of the improvement due to the discovery and adoption of the CRISPR/Cas9 system. This system entered the public consciousness in 2018 when a Chinese researcher announced using the system to create the first genetically edited human babies.

Systems for genome engineering are often introduced into target cells using plasmids. Mainly found in bacteria, natural plasmids are small, circular, mobile pieces of DNA that replicate independently from the host’s chromosomal DNA, and provide some benefit to the host, for example, resistance to antibiotics. Researchers now routinely design plasmids to study the function and expression of genes, for targeted delivery of medicines into cells, and recently for diagnostics. As a result, plasmids have become important for biological research, biomedicine, national security, and public health purposes.

Addgene, a nonprofit repository created to help scientists share plasmids, improves access to these materials and related information to accelerate research and discovery. During their quality control process, Addgene verifies all plasmids using short-read technology to ensure that only high-quality data and reagents are shared with the scientific community. However, short-read technologies require complex algorithms to assemble de novo (or piece together without a reference) the reads into the single character string that is the target DNA sequence. And de novo assembly of plasmids presents unique challenges, primarily due to the presence of repeated nucleotide sequences which are longer than the sequence reads. Although alternative, long-read sequencing technologies exist which produce read lengths on par with the length of typical plasmids, current versions of the devices, and chemistry, are not sufficiently production-ready for Addgene.

**Déjà Vu: The Novella**

Currently, no publicly available, automated assembly pipeline exists which is able to overcome the difficulties of de novo sequence assembly for plasmids. And so, in a project we call Déjà Vu: The Novella, Springbok worked with Addgene to explore how the problems caused by repeats for short-read assembly algorithms could be addressed. We aim to provide an effective, scalable solution to this problem in support of research, biomedicine, and national security mission needs.

In phase one of the project, we set out to collect curated plasmid sequences, and corresponding short-read sequencing data, in order to test candidate assemblers from which we could better understand the problems current algorithms encounter. Addgene's collection of curated sequences, manually inspected, or created, by a team of top-level scientists, is among the largest and best anywhere. Addgene collected all curated sequences, and short-read data, as well as the initial sequences produced by their sequencing provider, for all plasmids deposited during 2018. In total, 14,826 curated and initial sequences, and short-read data sets were collected.

Work by the scientist team at Addgene identified several candidate assemblers:

* SPAdes[^1], the St. Petersburg genome assembler [(https://github.com/ablab/spades)](https://github.com/ablab/spades)
* Shovill[^2], based on SPAdes [(https://github.com/tseemann/shovill)](https://github.com/tseemann/shovill)
* NOVOPlasty[^3], an organelle assembler and heteroplasmy caller [(https://github.com/ndierckx/NOVOPlasty)](https://github.com/ndierckx/NOVOPlasty)

And the Springbok team identified a number of other candidate assemblers:

* Unicycler[^4], also based on SPAdes [(https://github.com/rrwick/Unicycler)](https://github.com/rrwick/Unicycler)
* SKESA[^5], Strategic Kmer Extension for Scrupulous Assemblies [(https://github.com/ncbi/SKESA)](https://github.com/ncbi/SKESA)
* MaSuRCA[^6], the Maryland Super Read Cabog Assembler [(https://github.com/alekseyzimin/masurca)](https://github.com/alekseyzimin/masurca)

This set of assemblers provided a good selection of de Bruijn and overlap graph based assemblers, showed promising initial performance, and came recommended by researchers developing assemblers.

Given the scale of the data, and number of assemblers, we also realized that in order to process each of the collected short-read data sets for each of the six assemblers we needed to deploy each assembler either to a machine with many cores, or to a cluster of machines. Based on an earlier investigation at Addgene, the Springbok team selected [Toil, a scalable, pipeline management system written in Python](https://toil.ucsc-cgl.org/) developed at the UC Santa Cruz Genomics Institute. And in order to deploy assemblers to our development and processing environments we decided to use Docker containers.
 
**Biocontainers**

The first step in using Docker containers is to either find an image, or create a Dockerfile to build an image. In looking for a good source for both, the Springbok team identified Biocontainers, a community-driven project that provides the infrastructure and guidelines to create, manage and distribute bioinformatics packages (using Conda) and [containers (using Docker or Singularity)](https://biocontainers.pro). We liked the extensive list of tools (over 8,000), the partner organizations (like Bioconda, and Nextflow), and documentation. We customized the Biocontainers base image (based on Ubuntu 16.04) to include common processing and development resources. Then we standardized our Docker files, building software, when possible, and forking repositories, when needed for versioning.

**Toil**

We found Toil to be a great framework for prototyping a bioinformatics pipeline, especially for handling input and output files locally, or remotely, and scaling by using all available cores, or across a cluster. Files can be imported or exported locally, or from S3, just be using the correct scheme ("file", or "s3") in the file URL. Toil is not bound to any bioinformatics codebase, allows for defining task dependencies from within task methods, and offers a strong focus on cloud execution[^6]. And jobs can be run locally, on a remote instance, or on a remote cluster using Toil's cluster utilities. We isolated each tool to a custom job class, allowed data to be loaded from the local filesystem, or from S3, and provided a command line interface to each job. Finally, we used the Python unit testing framework to provide a test for each job.

**Results**

We deployed the assembler containers, and job classes to an EC2 c5.24xlarge instance with 96 vCPU. Happily, the 96 vCPUs mapped well to the short-read data sets which were organized by 96 well plate identifiers. Using our processing framework, we were able to assemble ten plates, or 960 plasmids, in one hour and 14 minutes. Truly light was the task where many shared the toil!

[^1]: Bankevich, Anton, Sergey Nurk, Dmitry Antipov, Alexey A. Gurevich, Mikhail Dvorkin, Alexander S. Kulikov, Valery M. Lesin, et al. “SPAdes: A New Genome Assembly Algorithm and Its Applications to Single-Cell Sequencing.” Journal of Computational Biology 19, no. 5 (May 2012): 455–77. https://doi.org/10.1089/cmb.2012.0021.
[^2]: Dierckxsens, Nicolas, Patrick Mardulyn, and Guillaume Smits. “NOVOPlasty: De Novo Assembly of Organelle Genomes from Whole Genome Data.” Nucleic Acids Research, October 24, 2016, gkw955. https://doi.org/10.1093/nar/gkw955.
[^3]: Wick, Ryan R., Louise M. Judd, Claire L. Gorrie, and Kathryn E. Holt. “Unicycler: Resolving Bacterial Genome Assemblies from Short and Long Sequencing Reads.” Edited by Adam M. Phillippy. PLOS Computational Biology 13, no. 6 (June 8, 2017): e1005595. https://doi.org/10.1371/journal.pcbi.1005595.
[^4]: Souvorov, Alexandre, Richa Agarwala, and David J. Lipman. “SKESA: Strategic k-Mer Extension for Scrupulous Assemblies.” Genome Biology 19, no. 1 (December 2018): 153. https://doi.org/10.1186/s13059-018-1540-z.
[^5]: Zimin, Aleksey V., Guillaume Marçais, Daniela Puiu, Michael Roberts, Steven L. Salzberg, and James A. Yorke. “The MaSuRCA Genome Assembler.” Bioinformatics 29, no. 21 (November 2013): 2669–77. https://doi.org/10.1093/bioinformatics/btt476.
[^6]: Leipzig, Jeremy. “A Review of Bioinformatic Pipeline Frameworks.” Briefings in Bioinformatics, March 24, 2016, bbw020. https://doi.org/10.1093/bib/bbw020.