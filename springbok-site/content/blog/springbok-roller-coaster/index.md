+++
title = "Our Dunning-Kruger Roller-Coaster"
date = "2022-04-06"
fragment = "content"
weight = 10
important = "true"
subtitle = "Raymond LeClair"

[asset]
    image = "dunning-kruger.jpg"
+++
Permission requested.

Ah, [Dunning-Kruger](https://en.wikipedia.org/wiki/Dunning%E2%80%93Kruger_effect), you are so cruel. You know, that psychological quirk of humans in which confidence starts high with lack of expertise, only to fall quickly, like on a stomach-wrenching roller-coaster, as knowledge is gained. Such was our recent project exploring surveillance using [genomic sequencing](https://en.wikipedia.org/wiki/Whole_genome_sequencing). While we knew we were far from experts in the field of genomic sequencing, we had high confidence that we would learn enough to accomplish something useful. Here is the story of how we did not. Sort of.

**Oxford Nanopore Technologies**

We set out to design a system using the Oxford Nanopore Technologies (ONT) portable DNA sample preparation device, the [VolTRAX](https://nanoporetech.com/products/voltrax), and portable DNA sequencing device, the [MinION](https://nanoporetech.com/products/minion), to automate edge sequencing of wastewater samples for genomic surveillance of novel pathogens such as bacteria and viruses.


Today, public-health surveillance relies on samples manually collected in clinical settings after symptom observation and analyzed using conventional laboratory techniques. This process takes time, and (typically) tests only for known pathogens. Furthermore, current practice fails to benefit from direct access to biological sequence information, which is particularly important for discovering novel organisms. As a result, it is difficult to quickly detect disease outbreaks due to novel pathogens. Some projects, such as Nextstrain, and Biobot, have emerged to address these limitations using genomics. Nextstrain is an open-source project that relies on samples collected from and prepared in research laboratories to track genomic variants globally, while Biobot analyzes data created from community wastewater samples. Unfortunately, Nextstrain relies on contributed sequence data, which prevents control of the sampling location, while Biobot uses short-read sequencing technology, which is problematic for identifying novel pathogens.


We hoped our project using ONT technology might be a small part of a genomic surveillance system for detecting novel pathogens before the next pandemic.

**MinION**

While the cost of [sequencing instruments](https://en.wikipedia.org/wiki/DNA_sequencehttps://en.wikipedia.org/wiki/Third-generation_sequencing) has fallen dramatically from their introduction, ONT technology is very low cost, at least for acquisition, and portable. Using the MinION, several groups have been successful in monitoring or responding to disease outbreaks in animals and humans.[^1][^2][^3][^4][^5]


The technology is one among several, so-called, [Third Generation Sequencing (TGS)](https://en.wikipedia.org/wiki/Third-generation_sequencing) technologies since it generates longer reads (median of 1754 bp (base pairs)) than Second Generation Sequencing (SGS) technologies (50-600 bp).[^6]


Here are the biological details of how it works. The fundamental technological unit of a MinION is a protein [nanopore](https://nanoporetech.com/how-it-works) set in an electrically resistant polymer membrane. An ionic current is passed through the nanopore by setting a voltage across this membrane. Then as a [DNA](https://en.wikipedia.org/wiki/DNA) molecule passes through the pore a characteristic disruption in current can be measured that makes it possible to identify the sequences of base pairs making up the molecule. These lengths are quite short biologically speaking, although they may sound impressive. For example, bacterial genomes range in size from 130 kbp to over 14 Mbp and viral genomes range in size from 1 kbp to 2.4 Mbp.


Whichever sequencing technology is used, an algorithm is required to assemble reads into the full DNA sequence since the reads are shorter than the sequence. Nevertheless, the read length of TGS technologies is often sufficient to enable genomic sequences to be assembled without a reference genome, which is often required for assembly. And that is why TGS technologies are so helpful for discovering novel pathogens.


For those savvy readers out there, you might say that the DNA molecule must be prepared in some fashion so that the MinION can do its work. And you would be right. This is something we didn’t fully appreciate when starting this project. The process, termed "library preparation", causes an adapter to bind to the DNA molecule which then attaches to the pore. ONT provides library preparation kits for this purpose once extracted and purified DNA molecules are available. Wait a minute, you say, which we should have done, from where did the extracted and purified DNA molecules arrive? There's the rub. Protocols for extracting and purifying DNA from various biological materials vary widely, though kits for this purpose are also widely available from multiple manufacturers. In addition, in the case of RNA viruses such as SARS-CoV-2, the virus which causes COVID-19, an extra step of RNA to DNA conversion is required. And so we had a blind spot, thinking of technology as electronic devices, or software algorithms, and failing to see these kits of liquids in bottles as the high technology many of them are.

**VolTRAX**

This is where we thought the VolTRAX would come to the rescue.  The VolTRAX was developed by ONT precisely to address the need for sample preparation.  With the VolTRAX, samples and reagents are manually added, then sample preparation proceeds in an automated manner, enabling reproducible and portable sample preparation. That, at least, was what the VolTRAX documentation suggested. However, in its iteration of 2021 or so, the VolTRAX is stable only for library preparation, and then, only certain libraries. At least according to the ONT representative with whom we discussed the project. It is at this point we pivoted to the Opentrons [OT-2](https://opentrons.com/ot-2) pipetting robot.

**Opentrons**

While automation for implementing molecular biology protocols has been available since at least the human genome project, to our knowledge, the OT-2 is the first small scale, inexpensive, modular device with a Python [API](https://en.wikipedia.org/wiki/API). The incumbent offerings seem to be large scale, often custom-built devices, more mainframe than laptop, and used in large centers rather than in edge clinics.


As we learned more about devices used to automate molecular biology protocols we realized: there is a human in the loop. It seemed to be a fundamental assumption of device designers that a human will be moving material between steps of a protocol. This prevents routine automation of the complete sequence of steps in a protocol. We think the modularity of the OT-2 is a good step toward addressing these concerns, and we remain intrigued with the OT-2. Apparently [OpenCell](https://blog.opentrons.com/how-opencell-is-scaling-up-covid-19-testing/) was as well,  since they partnered with King’s College and Opentrons to create an affordable shipping container COVID-19 testing lab. But it is only a step towards removing a person from the equation. In our view, the industry should move toward modular and interchangeable molecular biology instruments that would allow routine automation of complete molecular biology protocols.


As we sorted these equipment concerns, we began analyzing the system as a whole. Edge sequencing, if the edge is envisioned as locations for sampling municipal wastewater, requires many sequencing sensors. We realized the cost of sequencing consumables, especially flow cells for the MinION, would become prohibitive at useful spatial resolution. We decided we needed to re-envision the definition of edge sequencing to make this viable. In the end, given the ups and downs of the project roller-coaster so far, we decided to abandon our project. For now.


**Public Health Surveillance**

And what of Dunning-Kruger? Were we on the upswing, moving toward some knowledge justified confidence after hitting bottom? Well, it turns out the Dunning-Kruger effect (probably) doesn't even exist, being more of an artifact of statistics and presentation than a psychological reality.[^7] Then what of genomic surveillance? It is hardly forgotten, with the recent announcements that the Biden administration will invest $200M in genomic sequencing, and the Rockefeller Foundation will invest part of a recent $1 billion commitment in establishing a genomic surveillance network.  We join the National Security Commission on Artificial Intelligence call for global cooperation on smart disease monitoring. Stay tuned for updates as we chase this global cooperation.

**References**

[^1]: Butt, Salman L., Tonya L. Taylor, Jeremy D. Volkening, Kiril M. Dimitrov, Dawn Williams-Coplin, Kevin K. Lahmers, Patti J. Miller, et al. “Rapid Virulence Prediction and Identification of Newcastle Disease Virus Genotypes Using Third-Generation Sequencing.” Virology Journal 15, no. 1 (December 2018): 179. https://doi.org/10.1186/s12985-018-1077-5.


[^2]: Kafetzopoulou, L. E., S. T. Pullan, P. Lemey, M. A. Suchard, D. U. Ehichioya, M. Pahlmann, A. Thielebein, et al. “Metagenomic Sequencing at the Epicenter of the Nigeria 2018 Lassa Fever Outbreak.” Science 363, no. 6422 (January 4, 2019): 74–77. https://doi.org/10.1126/science.aau9343.


[^3]: Lemon, Jamie K., Pavel P. Khil, Karen M. Frank, and John P. Dekker. “Rapid Nanopore Sequencing of Plasmids and Resistance Gene Detection in Clinical Isolates.” Edited by Alexander Mellmann. Journal of Clinical Microbiology 55, no. 12 (December 2017): 3530–43. https://doi.org/10.1128/JCM.01069-17.


[^4]: Oude Munnink, B.B., M. Kik, N.D. de Bruijn, R. Kohl, A. van der Linden, C.B.E.M. Reusken, and M. Koopmans. “Towards High Quality Real-Time Whole Genome Sequencing during Outbreaks Using Usutu Virus as Example.” Infection, Genetics and Evolution 73 (September 2019): 49–54. https://doi.org/10.1016/j.meegid.2019.04.015.


[^5]: Rambo-Martin, Benjamin L., Matthew W. Keller, Malania M. Wilson, Jacqueline M. Nolting, Tavis K. Anderson, Amy L. Vincent, Ujwal Bagal, et al. “Mitigating Pandemic Risk with Influenza A Virus Field Surveillance at a Swine-Human Interface.” Preprint. Microbiology, March 21, 2019. https://doi.org/10.1101/585588.


[^6]: Weirather, Jason L., Mariateresa de Cesare, Yunhao Wang, Paolo Piazza, Vittorio Sebastiano, Xiu-Jie Wang, David Buck, and Kin Fai Au. “Comprehensive Comparison of Pacific Biosciences and Oxford Nanopore Technologies and Their Applications to Transcriptome Analysis.” F1000Research 6 (2017): 100. https://doi.org/10.12688/f1000research.10571.2.


[^7]: Nuhfer, Edward, Steven Fleisher, Christopher Cogan, Karl Wirth, and Eric Gaze. “How Random Noise and a Graphical Convention Subverted Behavioral Scientists’ Explanations of Self-Assessment Data: Numeracy Underlies Better Alternatives.” Numeracy 10, no. 1 (January 3, 2017). http://dx.doi.org/10.5038/1936-4660.10.1.4.