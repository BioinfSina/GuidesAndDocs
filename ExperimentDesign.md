# Experiment Design
### ~ What does your bioinformatician want you to know? ~
### Do your research before you do your research

## Table of contents
1. [Where to start](#start)
2. [Having a well-defined research question is important paragraph](#hypothesis)
3. [Ethical considerations](#ethics)
4. [Different types of replicates](#rep_type)
5. [How many replicates do you need?](#rep_number)
6. [What are good biological replicates?](#rep_biol)
7. [Different types of controls](#control_type)
8. [What is the best sequencing depth for my experiment?](#seq_depth)
9. [DNA/RNA concentration needed and how to deal with issues](#concentration)
10. [Confounding factors and how to deal with them](#confounder)
11. [How to avoid and deal with batch effects](#batch)
12. [Do I need to run another set of controls for each experiment?](#control_pub)
13. [Quasi-Experimental Design](#quasi)
14. [Pilot experiments provide insights into how to get the best results](#pilot)
15. [Human bias](#bias)
16. [Metadata](#metadata)
17. [Examples for good vs bad experiment design](#examples)
18. [Can’t I just use AI to plan my experiment?](#ai)
19. [Final remarks](#final)

<p align="center">
  <img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/expPlan.svg">
</p>

## Where to start
<a id="start"></a>
When designing an experiment, the first step is to define your [hypothesis](#hypothesis) or biological question. You can then identify the methods used to answer your question. These choices then lead to further choices about how the experiment might be designed.
With a hypothesis in mind, you should already start talking to collaborators and facilities that might be involved in the process, so they can help you make sensible choices about methodology and experimental design. For non-standard experiments you might need a [pilot experiment](#pilot) to test and practice different processes and to design the experiment to best answer your question
A successful pilot experiment helps you make informed decisions on necessary changes as well as deciding the [number](#rep_number) and [types](#rep_type) of replicates and [controls](#control_type) necessary for the main experiment. You can identify issues like [batch effects](#batch) and [confounding factors](#confounder) and need to adapt your design or analysis to appropriately deal with them. Once you are conducting your main experiment you will also need to collect appropriate [metadata](#metadata) to aid future analysis and reproducibility.
In this guide, we will talk about each step of experiment planning. It is, however, a general guide and each experiment will be different. This is not a substitute for consulting with us (<a href="mailto:bioinformatics@gurdon.cam.ac.uk">bioinformatics'at'gurdon.cam.ac.uk</a>) and other facilities to ensure the best results.


<a id="hypothesis"></a>
## Having a well-defined research question is important

With a vague goal in mind and abundant measurements and observations, you could try and get as much out of a single experiment as humanly possible. But would that really answer any questions properly?

In experiments, we can either follow a hypothesis-driven design, sometimes also called the ‘scientific method’, or a more observational, hypothesis-free design.
Hypothesis-driven design involves a research question, which is testable and allows you to design a well-defined and reproducible experiment to answer this specific question properly.
For example, if the hypothesis is that stem cells will proliferate more under condition 1 than under condition 2 you would grow them under both conditions and monitor proliferation. If the hypothesis is correct all (or at least a significant number) samples from condition 1 will be more proliferative than any of the samples under condition 2.
Having a good hypothesis is the optimal situation, but especially in sequencing-based experiments, people often take a more investigative approach, utilising a hypothesis-free design. This approach may seek to observe development, disease or the effect of a treatment over time, in multiple genetic backgrounds or environments, without a clear idea of what is expected The nature of ‘omics experiments means that you can get a good overview of, for instance, how expression of every gene changes and this can be useful for discovering new things about your biological system of interest. 
There might not be a defined hypothesis which you are testing, but you should take into account as much prior knowledge as possible to define which samples to collect. You should also expect to do further experiments to more specifically answer hypotheses generated by your initial experiment. A good hypothesis-free design should still have a primary focus and a clear end goal for your experiment.

<a id="ethics"></a>
## Ethical considerations

Good experiment design includes considering the ethical implications of your experiment. In vivo experiments can be done in a live animal model, donated human embryos or synthetic embryos created from stem cells. This comes with considerations of ethical use of these resources. In this case, detailed experiment design and [pilot experiments](#pilot) are even more important to make sure you have exactly as many replicates as necessary for good results and also avoid any unnecessary use of these resources.
Ethical considerations can limit the extent of your experiment, including number of replicates, strength of dosage (in life animals) or length of observation. For example there are clear limits on how long embryos can be grown or at what point you will have to sacrifice an animal if it is declining too rapidly.
Getting the appropriate approval is often a back and forth conversation with the approving body and involves discussing the feasibility of an experiment within ethical constraints. To speed up this process it is helpful to start with a well thought-through design and decisions informed by pilot experiments, legal guidelines, statistical power analysis and relevant publications.
Guidance on these matters is given by the Animal Welfare & Ethical Review Body (AWERB) [[1]](#1) and your departmental or institutional Research Ethics Committee.

<a id="rep_type"></a>
## Different types of replicates

We usually have two different types of replicates, technical and biological replicates.

<p align="center">
  <img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/replicate_types.svg">
</p>

Technical replicates are achieved by either sequencing the exact same sample multiple times or by splitting a sample into multiple (sub)samples. Those samples will then be separately processed through the same pipeline. This is done to ensure reproducible results and a consistent process. If you plan to include them based on worries about inconsistencies in the process it might be beneficial to do a [pilot study](#pilot) to make sure the potential variability and any necessary additional training, equipment maintenance or adaptation of the main experiment has been identified.
It is tempting to exclude technical replicates - which can be done for well-established protocols - but it is better to adapt analysis or repeat an experiment if the technical replicates showed issues, than to unknowingly publish irreproducible (and potentially wrong) results.

[Biological replicates](#rep_biol) are samples taken from multiple closely related sources that underwent the same treatment in the experiment. In an animal experiment that would mean sampling from multiple animals in the same treatment group. This ensures accounting for individual variation. Biological replicates need to be chosen so the variation between replicates does not overpower the variation you wish to measure. While technical replication is usually not necessary, biological replication is essential.

<a id="rep_number"></a>
## How many replicates do you need?

Statistically significant results can only be achieved with a hard minimum of 3 replicates. With two or fewer replicates it is not possible to access variability and estimate error for calculation of standard error and standard deviation. 
You should never collect fewer than three biological replicates per condition. With three replicates, you have the chance to spot outliers and swapped samples - two samples agreeing on a measurement and one disagreeing would indicate that the third one is an outlier. The outlier could then either be excluded - leaving only two samples with no significant mean result possible or kept - strongly affecting a mean or median of the group.  It is still not possible to decide if a single outlier has biological significance or not, hence it is generally better to include more than three replicates.
While in practice, three biological replicates is often sufficient to detect outliers and to find significant differences between your conditions, it is not actually enough to find all the real differences (false negatives) and exclude erroneous results (false positives). But how many do we need?

<p align="center">
  <img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/outliers.svg">
</p>

Schurch et al. (2016) [[2]](#2) discuss the necessary number of replicates to achieve good results in bulk RNASeq experiments. They see increases in true positives and decreases in false negatives until up to 40 replicates per group! Using appropriate analysis tools and fold change thresholds, they suggest 12 replicates per group are enough for high-quality results in bulk RNASeq.
12 replicates sounds like a lot, but we strongly suggest including at least 6 replicates to generate useful results. You need to consider that potentially not all of your replicates will pass sequencing and pre-processing quality control and some could be outliers. Outliers can be caused by unexpected biological variation like a rare genetic variant, by contamination or experimental error. If they are singular occurrences it can be necessary to exclude them, however if there are multiple outliers in a group it might be better to look into finding the exact cause and considering them showing valid variations.

Statistical power analysis gives you a mathematically supported number of replicates required to work with the expected variation. While it is a statistically sound tool, it is based on estimates for variation and effect size [[3]](#3), [[4]](#4). It can be difficult to define these estimates appropriately without [pilot experiments](#pilot). Hence, we suggest to go with a number of replicates known to work for technically and biologically similar experimental designs instead of doing a power analysis with questionable input estimates.

Cell lines generally have less variability, than for instance tissue samples from genetically divergent humans. While we advise to have at least 6 replicates per group, when working in a very controlled system like a cell line derived from the same individual this can be reduced down to the minimal three [[5]](#5). In general, higher variability requires more replicates to capture effects of the same size. Smaller effect sizes also require more replicates to be detected than larger effect sizes.
Using the appropriate number of biological replicates is crucial for ensuring the reliability and reproducibility of results. It allows you to capture variability, increase statistical power and confidence in findings, identify outliers and improve data quality - achieving robust and trustworthy results.



<a id="rep_biol"></a>
## What are good biological replicates?

Good biological replicates are based on being as biologically close to each other as possible without being the same. In an experiment on a cell line this might, for example, mean aliquoting your cells into 12 tubes, then treating half with a drug and half with just buffer. For a mouse experiment, that would mean using replicates with the same genetic background, the same age, from the same cages. There can be known variation in a group of replicates, for example including male and female mice or multiple genetic backgrounds, but in an optimal situation, those subgroups would be both equally distributed and have enough replicates amongst themselves to identify any effect based on their differences (a [confounding factor](#confounder)). So a good example is using 5 male and 5 female mice in one group, while a bad grouping would include 2 male and 8 female mice.
In the bad example, any effect only seen in male mice will not be able to be statistically distinguishable from the average.

When studying human disease it is often not possible to assign the treatment group randomly as it is by definition a group of patients with a given condition. These patients will have differing backgrounds and lifestyles. It is often helpful to go with  a [quasi-experimental design](#quasi) in those cases.

Another common problem is to define a biological replicate in regards to cell lines. One solution could be using multiple separate freezer stocks, which can be expensive or not feasible. The common solution for biological replicates in in vitro experiments is to maintain separate flasks of the same cells. However, the less variation you have between your replicates, the better you can determine detailed causal relationships or study smaller effect sizes.

<a id="control_type"></a>
## Different types of controls

The most commonly used control types are positive and negative controls. Positive controls get a treatment which is known to elicit the measured effect, while negative controls are usually untreated and should not show the studied effect at all. Negative controls act as a point of reference, allowing us to measure the size and direction of effects in our treatment groups. Positive controls can tell us whether the experiment has worked. If the positive control fails to show a result, then something went wrong with the experiment. If the positive control succeeded, but the treatment group shows no effect, we can be confident there really is no effect.

To define appropriate controls it’s important to know the potential for variability in the experiment. Higher variability will require more replicates to capture the full range of outcomes reliably and distinguish true biological variability from accidental outliers based on issues with the experiment or environmental influences. Controls should be spread over all batches to generate a baseline which doesn’t suffer a batch effect. Optimally control samples are chosen randomly, but can also be blocked to include the same diversity as the treatment groups to avoid [batch effects](#batch).
A simple example of this is how an allergy scratch test would be controlled by just scratching the skin without added substance for a negative control and a scratch with added histamine for a known reaction as a positive control to establish a baseline of reactivity for the patient.
For a bulk RNAseq experiment you might use treatment with a well known outcome as a positive control, for example treating with a cytokine and expecting up regulation of genes known to be triggered by this cytokine. This is only relevant if you are expecting and hoping to measure activation of the same pathway through other means in your treatment group.
Another form of control are mock treatment controls. In humans this could be a placebo instead of no treatment, in a cell line or model organism-based experiment this involves comparable handling of the controls and treatment groups, but without applying the treatment itself in the control, like mock injections with PBS [[6]](#6).
Preferably division into treatment and controls should be done without prior knowledge at the start of the experiment to avoid bias, for example choosing ‘stronger’ individuals for a treatment group to avoid having dropouts. 
Optimally control groups have just as many individuals as treatment groups, if this is not feasible they should still be statistically significant by including at least three replicates. In [quasi-experimental design](#quasi), control groups tend to be bigger than treatment groups to capture general population diversity.

<a id="seq_depth"></a>
## What is the best sequencing depth for my experiment?

It can be difficult to decide on proper sequencing depth for an experiment. Standard experiment designs can be compared to existing advice on sequencing depth - but it has to be kept in mind that advice on ‘reads per sample’ is usually only applicable to human or genomes with similar size and structure.

Some examples are:

* 20,000 read pairs per cell as a minimum in single-cell RNASeq for 10x Genomics sequencing [[7]](#7), but more for RNA-rich (e.g. tissues like spleen and thymus) samples or dependent on the questions asked, generally around 60,000 reads per cell for typical samples [[8]](#8)
* 25,000 read pairs per spot for Visium FFPE v1
* 25-50 M reads per sample for bulk RNASeq depending on the complexity of the sample
* Calculate based on coverage for whole genome sequencing (Coverage = read length * number of reads / genome size). 30-100x whole genome coverage is commonly used for calling variants based on Illumina short reads.

The final answer is dependent on your needs, the protocols and technology you are using, the organism sequenced, type of analysis you plan to do and financial constraints. Aim to have close to the numbers suggested, but don’t add a full sequencing run if you would achieve 90% of those numbers without it.
It is worth taking the complexity of the sample into account. A cell line is less complex than for example a tissue. If you are interested in a gene expressed at low level in a rare cell type within a tissue sample you would need more reads to detect it than a lowly expressed gene in a cell line. Increased sequencing depth is required for more complex samples.
For example if you have a human bulk RNASeq experiment with 5 treatment samples and 5 control samples, and you know that a good sequencing depth for a human bulk RNAseq is about 30M reads per sample because of the diverse transcriptome you would need to 30 M reads * 10 samples = 300 M reads in total. This amounts to nearly a full lane of sequencing on an Illumina NovaSeq 6000 using v1.5 chemistry (based on 350-450M reads per lane).

<a id="concentration"></a>
## DNA/RNA concentration needed and how to deal with issues 

The DNA/RNA concentration needed as input for sequencing library preparation depends on the library protocol used, the requirements requested by the sequencing provider and what you want to achieve with your data. In most cases, you can expect to need at least 150 ng of total RNA/DNA to achieve good results, but it might vary between 50 ng and 1 µg per sample.

Concentration can be measured with different methods, the most commonly used being NanoDrop, QuBit or Tapestation machines, or qPCR.

* NanoDrop is a simple spectrometry-based method that provides information on DNA, RNA, or protein concentration, as well as sample purity. It is quick, cheap, and easy to use, but it tends to overestimate DNA concentration.
* QuBit is based on fluorometry, measuring DNA or RNA concentration in a sample using their binding to a fluorescent dye. It is less affected by contaminants and generates more reliable measurements, especially at very low concentrations.
* Agilent TapeStation systems are based on electrophoresis. They analyse multiple samples in parallel and also generate a qualitative measurement, but are less reliable than a QuBit measurement.
* Quantitative PCR (qPCR) is the most accurate but most expensive and time-consuming method for DNA quantification. Rarely used for large-scale sequencing preparation.
 
Some sequencing providers require fluorometry-based readings to ensure the input requirements for their promised throughput results are met.

If you cannot achieve the optimal concentration for sequencing, there are a few options:

* Dilution: If samples have widely differing input concentrations, they should be diluted to a more unified input to ensure comparable results in multiplexed sequencing.
* Improving Extraction Protocol: If concentrations are generally too low, try to improve the extraction protocol. Pilot experiments are useful, especially if extracting from a tissue type or organism new to you.
* Increasing Input: Possibly increase the mass of the input material.
* PCR Cycles: If it is not possible to increase the extracted DNA or RNA, increasing the number of PCR cycles in library preparation is an option, but this must be documented to be able to troubleshoot resulting batch effects in the analysis process. Preferably all samples within an experiment should be subject to the same number of PCR cycles.

<a id="confounder"></a>
## Confounding factors and how to deal with them

Confounding factors include batch effects but are more general factors influencing the outcome of an experiment. They are connected both to the causal independent variable (e.g. treatment), and the dependent variable, which is the measured effect (e.g. gene expression levels). However, confounding factors are different from the independent variable. They are correlated with the independent variable and causally related to the dependent variable. This can make it impossible to distinguish the effect from being caused by the (observed or changed) independent variable or the correlated confounding factor. 

Confounding factors can be mitigated by using techniques like randomisation, where you don’t know what the confounding factors are, and blocking where you do. If that is not possible they can only be potentially discussed if they are part of the collected metadata.
If possible you would restrict your treatment and control group to only subjects with the same value for a confounding factor. For example only using male or female participants in studies where sex-related diseases or hormones can be confounding. However, this may restrict the generalisability of your experiment.

<a id="random"></a>
Randomisation is a way to reduce the impact of a known confounding factor. Individuals are randomly assigned to the treatment and control groups - which should lead to the confounding factors affecting both groups in the same way.

<a id="block"></a>
<p align="center">
  <img src="https://github.com/BioinfSina/GuidesAndDocs/blob/main/Pictures/blocking.svg">
</p>

A more direct method is blocking, where you allocate the same number of individuals affected by the same value of the confounding factor into all control and treatment groups, for example having age-matched controls or comparable numbers of male and female subjects to account for sex differences.

Blocking and randomisation control confounding variables, restriction avoids them and collecting abundant [metadata](#metadata) helps deal with them during analysis - especially for factors that were unknown during experiment design.


<a id="batch"></a>
## How to avoid and deal with batch effects

Optimally, all samples in your experiment are treated in exactly the same way, by the same person under fixed conditions at the same time. It’s rarely like that in reality, which introduces batch effects. Batch effects are a subset of [confounding factors](#confounder) caused by technical factors like using multiple reagent batches or changing personnel.
Methods to avoid and deal with batch effects by adapting the experiment design are [randomisation](#random) and [blocking](#block).
Some batch effects cannot be avoided. For example, if you are conducting a longitudinal study to investigate the progression of a disease over several years, collecting blood samples from patients at multiple time points: baseline, 1 year, 2 years, and 5 years. The technology and equipment used for sample processing and analysis evolve, leading to differences in the data generated at each time point. Even if you can keep the equipment the same, it will have been maintained multiple times throughout the experiment, and reagents will come from different batches, as they do not keep long enough. In this scenario, batch effects are introduced by the changes in technology, reagents, and equipment over the years and you cannot avoid the effect caused by these changes.
Other batch effects can be mitigated controlling how they affect the results through experiment design. Having to sequence samples over multiple runs could introduce a batch effect per run, but if you randomise which samples will be on each run and ensure running an even amount of samples from each experimental group each time, this might still introduce a measurable batch effect, but it will not obscure your results from comparing conditions. Alternatively, all samples could be sequenced at lower depths on each of the runs, resulting in multiple technical replicates per sample, which are merged for analysis.

Batch effects that can not be avoided through those methods or were unknown until data analysis uncovered them can sometimes be algorithmically controlled or corrected during analysis  [[9]](#9). This usually requires the availability of unaffected controls or samples to correct for the batch effect. Methods not based on using information from unaffected samples as a baseline are available but can potentially introduce another bias or only change the bias from the batch effect to be less noticeable. They could obscure actual biological variation by overcorrection. Hence, if it is not possible to avoid or correct the batch effect during experiment design, it might be advisable to leave it in and discuss it using the appropriate metadata for reference, taking known biological effects into account.

Dealing with batch effects that couldn’t be avoided in the analysis is often done through specific toolkits, for example Harmony [[10]](#10) (for scRNAseq or spatial transcriptomics) and ComBat [[11]](#11) for bulk RNASeq.


<a id="control_pub"></a>
## Do I need to run another set of controls for each experiment?

It can be tempting to reuse controls from a previous experiment or published data. However, this approach has multiple problems. Even with controls from a comparable previous experiment in the same lab there will still be a significant potential for a [batch effect](#batch) from the control being processed at a different time, with a different batch of reagents, by a different person. Published data will have all these confounding factors, plus potentially different genotypes, different experimental protocols, different library preparation kits and different sequencing machines. Therefore, it is never advisable to forego controls in your current experiment.

<a id="quasi"></a>
## Quasi-Experimental Design

If the treatment group is impossible to [randomise](#random) - for example patients with a specific disease - you can utilise a quasi-experimental design to define [control groups](#control_type) in a way that allows controlling for [confounding factors](#confounder).
There can be inherent confounding factors, like risk factors of a studied disease. For example, a study group with lung cancer would include a larger number of smokers than expected in the general population. Even if a similar number of smokers can be added to the control group, healthy smokers have increased risk of having undiagnosed lung cancer or precancerous lesions based on this risk factor.
The quasi-experimental design relies either on carefully matched controls or covering the expected diversity of a relevant group or the general population though large control groups. Matching controls can include age, sex, gender, ethnicity, environment, genetics (family members), disease status for a set of related diseases, risk factors and more depending on your patient group. Finding an appropriate control group can be difficult and will usually come with some compromise. Hence, healthy control groups are often much larger than the patient group to cover the general population diversity without matching each patient.

<a id="pilot"></a>
## Pilot experiments provide insights into how to get the best results

Pilot experiments are small-scale studies conducted before the main experiment. They are crucial for refining and improving the design of your main study.
A pilot experiment can be used to assess the feasibility of the experiment, test and practice the procedures, and generate example data for analysis. They help determine the amount of expected variation and thus ensure the number and type of replicates and controls collected are appropriate. They can be used to determine what is an appropriate sequencing depth and to determine the number of cells you need to collect for a scRNA-seq experiment so you can analyse a rare cell population.
 
Conducting pilot experiments can save you money in the long run by optimising the experiment design and ensuring you have the right training and analysis tools available before starting a larger experiment. This way, you maximise the outcomes of the main experiment without risking a loss of time and resources.

The design of a pilot experiment involves reducing your number of samples to a ‘minimal example’. However, for a single-cell RNA-seq experiment you might aim to sequence a large number of cells at high depth, to determine the optimal number of cells and [sequencing depth](#seq_depth) on the full set of samples in the main experiment.


<a id="bias"></a>
## Human bias

Bias is ever present in our world and experimental designs. Just like asking someone suggestive questions can ensure getting the answer you want, bias can also influence experiments. Biased experiments lead to biased results which cannot be replicated.
It sounds convenient if a pilot experiment showed you the expected results for 4 out of 6 genetic backgrounds to omit the unexpected ones in the main experiment and get a cleaner result. This is a valid choice and can make publication easier, but a less biased solution would be to  discuss the [pilot experiment](#pilot) results in the publication and argue why you have been focussing on the selected backgrounds. Otherwise, an experiment might give the implication that it is generalisable even though biased selection is only making it seem so.

There can also be subconscious biases. For example, choosing a cell line you have previously worked with over one that is objectively more appropriate because you have more experience with it. Similarly, when working with multiple cell lines or technologies in the same experiment, ones you have more experience with can give you better results than ones you are working with for the first time. To avoid biased choices and results, additional training and pilot experiments are helpful.
Subconscious bias is also well know to be present in experiments with human participants, leading to placebo or nocebo effect in patients or biased treatment by researchers or health care personnel. This is why we introduce blinding - either of the researchers and care personnel, the patients or optimally both.
It is important to talk through experiment design with colleagues who can point out subconscious bias to you. 

<a id="metadata"></a>
## Metadata

Metadata provide context for your data and ensure reproducibility. There are standardised rules for metadata necessary to publish and upload data in the appropriate databases [[12]](#12), but it is also very important to collect as much metadata as possible for better analysis.
Metadata can help identify [confounding factors](#confounder) during analysis and underpin the biological validity of your results.
It is important to document metadata consistently and through standardised measures. However, it can also be helpful to keep general notes and observations during the course of an experiment as metadata.
Types and examples of metadata include sample-associated metadata (sampling time, genetic background, age, disease status), preparation metadata (sampling protocol, RNA extraction, number of PCR cycles, RIN numbers, library prep), experimental metadata (observations and changes, behaviour) and analysis metadata (analysis workflow, software versions, necessary curation steps, exclusion of outliers).

<a id="examples"></a>
## Examples for good vs bad experiment design

### Bulk RNASeq mouse experiment

**Objective:** Investigate the effect of a new injected drug on gene expression in mice

#### Design
**Treatment Group:** Mice injected with the drug  
**Mock Treatment [Control](#control_type):** Mice injected with PBS  
**Negative Control:** Healthy mice not injected with either   

#### Challenges	
**Known [Batch Effect](#batch):** Experiment needs two days of RNA extraction and multiple sequencing runs

**[Confounding Factor](#confounder):** Age of the mice

#### Good Experimental Design:

* [Randomisation](#random): Randomly assign mice to each group at the start of the experiment to minimise selection bias
* [Replication](#rep_number): Include five biological replicates for each group 
* [Blocking](#block): Distribute equal numbers of samples from each group on both extraction days and all sequencing runs
* Blinding: Animal facility staff are blinded to the group assignments to reduce chances of [biased](#bias) treatment
* Control for [Confounding Factors](#confounder): Use age- and sex-matched mice for all groups to control for variability

Sequence each sample to a [depth](#seq_depth) of 25-30 million reads to enable differential expression analysis of known mouse genes.


#### Issues to avoid (bad design):

* Lack of Randomisation: Selecting stronger mice for the treatment group
* No Replication: Use only two mice per group, making the results unreliable and statistically invalid for analysis
* Ignoring Batch Effects: Each group has RNA extraction on a separate day and is sequenced on a separate run
* No Blinding: Staff know the group assignments, potentially causing biased behaviour.
* Confounding Factors: Use younger mice for treatment group and older ones as negative control, all male mice are in mock treatment group

### Working with patients - [Quasi-experimental design](#quasi)

**Objective:** Evaluate the impact of a new medication on the methylation patterns in patients with lung cancer.

#### Design:
**Intervention Group:** Patients with lung cancer who receive the new medication
**Standard Care Group**: Patients with lung cancer who receive the current standard of care
**Control Group:** Healthy individuals

#### Challenges:
**Smoking as a Confounding Factor:**  
Issue: Smokers are more prevalent in lung cancer patients than in the general population. If the control group has fewer smokers than the intervention groups, it could skew the results. Cancer is more likely to develop later in life.   
Solution: Ensure all groups have a similar proportion of smokers to control for this variable and have the same age range.

**Risk of Pre-Cancerous Lesions or Undiagnosed Lung Cancer in Smokers:**   
Issue: Smokers in the control group might have pre-cancerous lesions or undiagnosed lung cancer  
Solution: Detailed health checks for the control group to remove individuals at risk

A larger control group might be necessary to take into account potentially having to remove participants from the control if they develop lung cancer, keeping enough participants for statistically relevant results.
[Sequencing depth](#seq_depth) is highly dependent on your financial constraints, as sequencing required for methylation analysis tends to be more expensive. It could be advisable to do targeted sequencing of selected regions of interest.

<a id="ai"></a>
## Can’t I just use AI to plan my experiment?

AI can assist you with planing steps like the data analysis, but often gives very generalised advice. While it is helpful to get started or find known issues with a design or workflow you are planning to use, it is no match for human professionals. If you struggle with experiment design, talk to your colleagues and friendly core facility staff before haggling with a large language model that might or might not give you advice appropriate for your specific needs. If you have used AI in planning please cross-check your results with human experts.

<a id="final"></a>
## Final remarks

A lot of information on experiment design is based on a perfect world where your resources are unlimited and your choices only affected by optimal experiment design. We have aimed in this guide to give realistic and feasible advice. Realistically, there will be decisions made based on funding availability, time restrictions, practicality and availability of equipment and expert knowledge. In this case discussing with experts how to achieve the best design under given constraints is important.
Contact us (<a href="mailto:bioinformatics@gurdon.cam.ac.uk">bioinformatics'at'gurdon.cam.ac.uk</a>) if you would like to discuss your experiment.

## References

<a id="1">[1]</a>
‘Animal Welfare & Ethical Review Body’. 6 February 2015. https://www.ubs.admin.cam.ac.uk/animal-welfare-ethical-review-body.

<a id="2">[2]</a>
Schurch, Nicholas J., Pietá Schofield, Marek Gierliński, Christian Cole, Alexander Sherstnev, Vijender Singh, Nicola Wrobel, et al. ‘How Many Biological Replicates Are Needed in an RNA-Seq Experiment and Which Differential Expression Tool Should You Use?’ RNA 22, no. 6 (June 2016): 839. https://doi.org/10.1261/rna.053959.115.

<a id="3">[3]</a>
Peterson, Sarah J., and Sharon Foley. ‘Clinician’s Guide to Understanding Effect Size, Alpha Level, Power, and Sample Size’. Nutrition in Clinical Practice 36, no. 3 (2021): 598–605. https://doi.org/10.1002/ncp.10674.

<a id="4">[4]</a>
Steidl, Robert J, and Len Thomas. ‘Power Analysis and Experimental Design’. In Design and Analysis of Ecological Experiments, edited by Samuel M Scheiner and Jessica Gurevitch, Second Edition., 14–36. Oxford University PressNew York, NY, 2001. https://doi.org/10.1093/oso/9780195131871.003.0002.

<a id="5">[5]</a>
Broman, Karl W. ‘Experimental Design and Sample Size Determination’. https://www.biostat.wisc.edu/~kbroman/talks/acuc_ho.pdf.

<a id="6">[6]</a>
Conn, Vicki S., and Tamara Coon Sells. ‘Compared to What?’ Western Journal of Nursing Research 42, no. 9 (1 September 2020): 772–73. https://doi.org/10.1177/0193945916650392.

<a id="7">[7]</a>
10X Genomics. ‘What Is the Recommended Sequencing Depth for Single Cell 3’ and 5’ Gene Expression Libraries?’ Accessed 17 March 2025. https://kb.10xgenomics.com/hc/en-us/articles/115002022743-What-is-the-recommended-sequencing-depth-for-Single-Cell-3-and-5-Gene-Expression-libraries.

<a id="8">[8]</a>
Settles, Dr Matthew L. ‘Single-Cell Transcriptomics’, https://ucdavis-bioinformatics-training.github.io/2017-June-RNA-Seq-Workshop/friday/scRNAseq.pdf.

<a id="9">[9]</a>
Yu, Ying, Yuanbang Mai, Yuanting Zheng, and Leming Shi. ‘Assessing and Mitigating Batch Effects in Large-Scale Omics Studies’. Genome Biology 25, no. 1 (3 October 2024): 254. https://doi.org/10.1186/s13059-024-03401-9.

<a id="10">[10]</a>
Korsunsky, Ilya, Nghia Millard, Jean Fan, Kamil Slowikowski, Fan Zhang, Kevin Wei, Yuriy Baglaenko, Michael Brenner, Po-ru Loh, and Soumya Raychaudhuri. ‘Fast, Sensitive and Accurate Integration of Single-Cell Data with Harmony’. Nature Methods 16, no. 12 (December 2019): 1289–96. https://doi.org/10.1038/s41592-019-0619-0.

<a id="11">[11]</a>
Zhang, Yuqing, Giovanni Parmigiani, and W Evan Johnson. ‘ComBat-Seq: Batch Effect Adjustment for RNA-Seq Count Data’. NAR Genomics and Bioinformatics 2, no. 3 (1 September 2020): lqaa078. https://doi.org/10.1093/nargab/lqaa078.

<a id="12">[12]</a>
National Microbiome Data Collaborative. ‘Introduction to Metadata and Ontologies’. Accessed 17 March 2025. https://microbiomedata.org/introduction-to-metadata-and-ontologies/.
