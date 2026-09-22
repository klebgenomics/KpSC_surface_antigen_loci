<img align="right" src="https://github.com/klebgenomics/Kaptive/blob/master/docs/assets/logo.png?raw=true" alt="Kaptive" width="200">

# _Klebsiella pneumoniae_ Species Complex surface polysaccharide locus databases

[![Streamlit App](https://img.shields.io/badge/Streamlit-%23FE4B4B.svg?logo=streamlit&logoColor=white)](https://kaptive-database-validator.streamlit.app/)
[![Database CI/CD Pipeline](https://github.com/klebgenomics/KpSC_surface_antigen_loci/actions/workflows/release.yml/badge.svg)](https://github.com/klebgenomics/KpSC_surface_antigen_loci/actions/workflows/release.yml)

This repository houses databases for _in silico_ typing of _K. pneumoniae_ Species Complex (KpSC) K and O surface polysaccharides using [Kaptive](https://github.com/klebgenomics/Kaptive). The capsule polysaccharide (K) and outer-lipopolysaccharide (O) are major surface antigens and phage binding receptors, making them key targets for novel vaccines, monoclonal antibody and phage therapies targeting KpSC.

Genomic typing approaches have helped reveal extensive K and O polysaccharide variation among natural KpSC populations, and power large scale seroepidemiology analyses. To learn more about genomic analyses and seroepidemiology of KpSC, check out the training materials [here](https://github.com/klebgenomics/KlebNetTrainingSep2025). 

> [!WARNING]
> These databases should not be used for species outside of the KpSC! Using the databases to type other organisms, including other _Klebsiella_ species, may result in errors and low typing rates. 

> [!TIP] 
> K and O locus databases for the _Klebsiella oxytoca_ Species Complex are available [here](https://github.com/klebgenomics/KoSC-surface-antigen-loci).

## Contents
- [What is the _K. pneumoniae_ Species Complex?](#what-is-the-k-pneumoniae-species-complex)
- [Database formats and versions](#database-formats-and-versions)
  - [How are loci defined?](#how-are-loci-defined)
  - [K locus database](#k-locus-database)
    - [K loci](#k-loci)
    - [Predicted K types](#predicted-k-types)
    - [Database versions](#database-versions)
    - [Changes to the K locus database](#changes-to-the-k-locus-database)   
  - [O locus database](#o-locus-database)
    - [O loci](#o-loci)
    - [Predicted O types](#predicted-o-types)    
- [Citations](#citations)
- [Curators](#curators)
- [Contribute](#contribute)
- [License](#license)

## What is the _K. pneumoniae_ Species Complex?

The _K. pneumoniae_ Species Complex (KpSC) comprises _K. pneumoniae_ and closely related organisms that cannot be accurately distinguished by standard biochemical or mass-spectometry-based identification protocols (see table and phylogeny below). We've included the phylogroup numbers in the table below for backwards compatibility with older literature, but these names are no longer recommended for use. See [this review]( https://www.nature.com/articles/s41579-019-0315-1) for an overview of the species complex. 

| Species                                       | Kp phylogroup<sup>a</sup> | Kp phylogroup (alternative)<sup>b</sup> | Reference                                                                                                                                                                               |
|-----------------------------------------------|---------------------------|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *K. pneumoniae*                               | Kp1                       | KpI                                     | [Brenner, D.J. 1979 Int J Syst Evol Microbiol 29: 38-41](https://ijs.microbiologyresearch.org/content/journal/ijsem/10.1099/00207713-29-1-38)                                           |
| *K. quasipneumoniae* subsp *quasipneumoniae*  | Kp2                       | KpIIa                                   | [Brisse et al., 2014 Int J Syst Evol Microbiol 64:3146-52](https://ijs.microbiologyresearch.org/content/journal/ijsem/10.1099/ijs.0.062737-0#tab2)                                      |
| *K. quasipneumoniae* subsp *similipneumoniae* | Kp4                       | KpIIb                                   | [Brisse et al. 2014 Int J Syst Evol Microbiol 64:3146-52](https://ijs.microbiologyresearch.org/content/journal/ijsem/10.1099/ijs.0.062737-0#tab2)                                       |
| *K. variicola* subsp *variicola*              | Kp3                       | KpIII                                   | [Rosenblueth et al. 2004 Syst Appl Microbiol 27:27-35](https://www.sciencedirect.com/science/article/abs/pii/S0723202004702349?via%3Dihub)                                              |
| *K. variicola* subsp *tropica*                | Kp5                       | <span class="title-ref">-</span>        | [Rodrigues et al., 2019 Res Microbiol ﻿S0923-2508:﻿30019-1](https://www.sciencedirect.com/science/article/pii/S0923250819300191?via%3Dihub) (described as subsp *tropicalensis* in paper) |
| *K. quasivariicola*                           | Kp6                       | <span class="title-ref">-</span>        | [Long et al. 2017 Genome Announc 5: ﻿e01057-17](https://mra.asm.org/content/5/42/e01057-17)                                                                                              |
| *K. africana*                                 | Kp7                       | <span class="title-ref">-</span>        | [Rodrigues et al. 2019 Res Microbiol ﻿S0923-2508:﻿30019-1](https://www.sciencedirect.com/science/article/pii/S0923250819300191?via%3Dihub) (described as *africanensis* in this paper)    |

<sup>a</sup> Kp phylogroup numbers as described in [Rodrigues et al.
2019](https://www.sciencedirect.com/science/article/pii/S0923250819300191?via%3Dihub)

<sup>b</sup> alternative (older) Kp phylogroup numbers as described in
[Brisse et al.
2001](https://ijs.microbiologyresearch.org/content/journal/ijsem/10.1099/00207713-51-3-915#tab2)
and [Fevre et al. 2005](https://aac.asm.org/content/49/12/5149) prior to
the identification of *K. variicola* subsp *tropica*, *K.
quasivariicola* and *K. africana*.

![Unrooted phylogeneny showing the relationships between Klebsiella species and other selected Enterobacteriales, with KpSC marked](/images/Enterobacteriales_tree_KpSC.png)


## Database formats and versions

The K and O locus databases each comprise two files that are required to run Kaptive:
1. A multi-genbank file containing each unique locus sequence and its gene annotations.
2. A metadata file in TOML format, which provides essential information about the database (e.g. version, target organism(s), curator details), plus any special [phenotype logic](https://klebgenomics.github.io/Kaptive/db/curation.html#phenotype-logic) that applies to the database.

Please see the [Kaptive docs](https://klebgenomics.github.io/Kaptive/db/curation.html) for more details on the database file formats.

### How are loci defined?

Loci are defined by the rules of the [Kaptive typing framework](https://klebgenomics.github.io/Kaptive/Databases.html#what-is-a-locus), which states that **a unique locus should represent a unique set of genes**, with the assumption that this encodes a unique
polysaccharide structure. In many cases, these unique structures will
result in unique immunological serotypes. 

The gene translations (protein sequences) from each locus are compared
by pairwise alignment, and must fall under a defined percent identity
threshold to be considered 'unique'. Some genes (such as the core
assembly machinery) will be highly similar, however the genes
responsible for the polysaccharide structural diversity are expected to
be more variable. **The gene identity threshold for the 
KpSC databases is 82.5%.**

In some cases, specific nucleotide variations within loci and/or additional genes located elsewhere in the genome are known to result in modifications to the resulting polysaccharide structure. Where the impact of these variations or additional genes is well understood, they are captured within the databases using the phenotype logic section of the metadata file and the 'extra genes' entries within the multi-genbank file (see below for examples).

### K locus database

#### K loci

The KpSC [K locus reference database](https://github.com/klebgenomics/KpSC_surface_antigen_loci/blob/main/Klebsiella_pneumoniae_Species_Complex_K.gbk)
(`Klebsiella_pneumoniae_Species_Complex_K`) comprises full-length
(*galF* to *ugd*) annotated sequences for each distinct KpSC K
locus, where available:

- K loci KL1-KL72, KL74 and KL79-KL82 correspond to the loci of the original _Klebsiella_ serotype reference strains (sequences described [here](https://doi.org/10.1038/srep15573)).  K1-K72, K74 and K79-K82, respectively.
- KL101 and above were defined from DNA sequence data on the basis of
  gene content, numbered by order of discovery. At the time of discovery, no matched phenotypes were known. 

> [!Note]
> Insertion sequences (IS) are excluded from this database since we assume that the ancestral sequence was likely IS-free and IS transposase genes are not specific to the K locus.
> Synthetic IS-free K locus sequences were generated for K loci for which no naturally occurring IS-free variants have been identified to date.

#### Predicted K types

K phenotypes are annotated in the database for those loci where corresponding serological types and/or polysaccharide structures have been defined. These phenotype predictions are reported in the Kaptive output as the `Best match type`.

- K1-K72, K74 and K79-K82 were defined through serological typing techniques in the 1950s-1970s (see [Edwards and Fife JID 1952](https://doi.org/10.1093/infdis/91.1.92); [Edmunds JID 1954](https://doi.org/10.1093/infdis/94.1.65); [Ørskov and Fife-Asbury Int. J. Syst. Evol. Microbiol. 1977](https://doi.org/10.1099/00207713-27-4-386)) and correspond to K loci KL1-KL72, KL74 and KL79-KL82, respectively.
- K37 was defined through serological typing (see papers above), and the type strain was subsequently [shown to carry](https://doi.org/10.1038/srep15573) a K locus with high similarity to that of the K22 type strain, with the key difference being a truncation in an acetyltransferase gene that results in loss of acetyl modification from the capsule. Kaptive therefore predicts the K37 phenotype when it detects the KL22 locus with a truncated acetyltransferase gene. 
- K102, K112, K122, K136 and K149 serotypes were defined more recently in this [Technical Note](https://zenodo.org/records/15742130) and correspond to KL102, KL112, KL122, KL136 and KL149, respectively.

> [!TIP] 
> Kaptive will report `Best match type` as `Capsule null` when it identifies a truncation in an essential capsule synthesis / assembly gene e.g. _wza_, _wzb_, _wzc_, _wzx_ and/or _wzy_, or an initiating glycosyltransferase gene, _wcaJ_ or _wbaP_.

#### Database versions:

- v0.5.1 and below (previously distributed with Kaptive) include the original KpSC K
  locus databases, as described in [Wyres, K. et al. Microbial Genomics
  2016.](http://mgen.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000102)
- v0.6.0 and above (previously distributed with Kaptive) include four novel KpSC K
  locus references (KL162-KL165), described in
  [Wyres et al. Genome Medicine
  2020](https://pubmed.ncbi.nlm.nih.gov/31948471/).
- v0.7.1 and above (previously distributed with Kaptive) contain updated versions of the KL53 and
  KL126 loci (see table below for details). The updated KL126 locus
  sequence is described in [McDougall, F. et al. Research in
  Microbiology 2021](https://pubmed.ncbi.nlm.nih.gov/34506927/).
- v0.7.2 and above (previously distributed with Kaptive) include a novel K locus
  reference (KL166), described in
  [Le, MN. et al. Microbial Genomics
  2022](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000827).
- v0.7.3 and above (previously distributed with Kaptive) include four novel K
  locus references (KL167-KL170),
  described in [Gorrie, C. et al. Nature Communications
  2022.](https://www.nature.com/articles/s41467-022-30717-6)
- v2.0.0 and above (previously distributed with Kaptive) include 16 novel K locus
  references (KL171-KL186) and
  described in [Lam, M.M.C et al. Microbial Genomics
  2022.](https://doi.org/10.1099/mgen.0.000800)
- v3.0.0 and above (previously distributed with Kaptive), the original KL37 locus was removed since under the Kaptive typing framework, this locus is identical to KL22 (i.e. they contain the same set of genes), differing only by a frameshift mutation in an aceytyltransferase gene which results in the loss of an acetyl group from the K37 polysaccharide structure. From v3.0 onwards we include an explicit prediction of the K37 phenotype based on the presence of the KL22 locus with truncated acetyltransferase. Kaptive will report these genomes as `Best match locus: KL22`, `Best match type: K37`. 
- v3.2.0 and above (previously distributed with Kaptive) introduced a re-annotation of the K
  locus reference genes curated by Dr. Tom Stanton and A/Prof Johanna
  Kenyon. All K-locus genes where thoroughly screened against curated
  annotations with a variety of homology detection methods to provide a
  more accurate functional description and standardised gene nomenclature.

> [!Tip]
> You can see a full list of database versions in this repository [here](https://github.com/klebgenomics/KpSC_surface_antigen_loci/tags). The version displayed/downloaded by default is the most recent version (highest number).

#### Changes to the K locus database

| Locus | Change | Reason | Date of change | Version |
|----|----|----|----|----|
| KL53 | Annotation update: *wcaJ* changed to *wbaP* | Error in original annotation | 21 July 2020 | v 0.7.1 |
| KL126 | Sequence update: new sequence from isolate FF923 includes *rmlBADC* genes between *gnd* and *ugd* | Assembly scaffolding error in original sequence from isolate A-003-I-a-1 | 21 July 2020 | v 0.7.1 |
| KL37 | Removed from the database | Locus is a deletion (atr) variant of KL22 | 22 March 2024 | v 3.0.0 |
| All | Updated gene names and functional annotations | Database standardisation | March 2026 | v 3.2.0 |

### O locus database

#### O loci

The [O locus database](https://github.com/klebgenomics/KpSC_surface_antigen_loci/blob/main/Klebsiella_pneumoniae_Species_Complex_O.gbk) (`Klebsiella_pneumoniae_SC_O.gbk`) includes the full length annotated sequences for all known KpSC O loci.

From v3.1.0, we introduced new O locus and O antigen nomenclature along with the publication
of this review: [O-antigen polysaccharides in Klebsiella pneumoniae:
structures and molecular basis for antigenic
diversity](https://journals.asm.org/doi/full/10.1128/mmbr.00090-23#T1).

We have also summarised the O-antigen nomenclature update on the [Wyres
Lab
website](http://wyreslab.com/klebsiella-pneumoniae-o-antigen-genetics-structural-diversity-and-nomenclature/).

> [!Tip]
> You can see a full list of database versions in this repository [here](https://github.com/klebgenomics/KpSC_surface_antigen_loci/tags). The version displayed/downloaded by default is the most recent version (highest number).

#### Predicted O types

O polysaccharide structures are known and/or predicted for all O loci; however, O classification requires some special logic. In particular, the O1 and O2 polysaccharides are associated with the same O loci and the distinction between O1 and each of the defined O2 subtypes (2α, 2β, 2γ) is determined by the presence/absence of 'extra genes' (_gml2β_ and _orf8_) elsewhere in the chromosome as indicated in the table below. Kaptive therefore looks for these genes to predict antigen (sub)types. You can find information about the database versions <3.1.0 [here](https://github.com/klebgenomics/KpSC_surface_antigen_loci/blob/main/Legacy%20Database%20Information%20%E2%80%94%20Kaptive%203.2.0%20documentation.pdf).


| New serotype designation | Required genes/loci (implemented in v.3.1+) | Prior designation (v.2.0.8–v.3.0.0b6) | Prior genes/loci (v.2.0.8–v.3.0.0b6) |
|----|----|----|----|
| O1αβ,2α | OL2α.(1/2/3), wbbYZ | O1ab | O1/O2v1, wbbYZ |
| O1α,2α | OL2α.(1/2/3), wbbY | O1a | O1/O2v1, wbbY |
| O1αβ,2β | OL2α.(1/2/3), gml2β, wbbYZ | O1ab | O1/O2v2, wbbYZ |
| O1α,2β | OL2α.(1/2/3), gml2β, wbbY | O1a | O1/O2v2, wbbY |
| O1αβ,2γ | OL2α.(1/2/3), orf8, wbbYZ | O1ab | O1/O2v3, wbbYZ |
| O2α | OL2α.(1/2/3) | O2a | O1/O2v1 |
| O2β | OL2α.(1/2/3), gml2β | O2afg | O1/O2v2 |
| O2αγ | OL2α.(1/2/3), orf8 | O2a | O1/O2v3 |
| O3α + O3β | OL3α/β | O3/O3a | O3/O3a |
| O3γ | OL3γ | O3b | O3b |
| O4 | OL4 | O4 | O4 |
| O5 | OL5 | O5 | O5 |
| O10 | OL10 | OL103 | OL103 |
| O11αβ,2α | OL2α.(1/2/3), wbmVWX | O2ac | O1/O2v1, wbmVWX |
| O11α,2α | OL2α.(1/2/3), wbmVW | O2ac | O1/O2v1, wbmVW |
| O11αβ,2β | OL2α.(1/2/3), gml2β, wbmVWX | O2ac | O1/O2v2, wbmVWX |
| O11α,2β | OL2α.(1/2/3), gml2β, wbmVW | O2ac | O1/O2v2, wbmVW |
| O11αβ,2γ | OL2α.(1/2/3), orf8, wbmVWX | O2ac | O1/O2v3, wbmVW |
| O12 | OL12 | O12 | O12 |
| O13 | OL13 | O13 | OL13 |
| O14 | OL14 | OL102 | OL102 |
| O15 | OL15 | OL104 | OL104 |

> [!Note]
> O3α and O3β are mannose containing polysaccharides that differ by the number of mannose residues within each polysaccharide repeat unit. The specific genetic determinants driving these length differences are not yet known, so Kaptive reports these O types together.


## Citations

If you use the K locus database please cite:

Wyres _et al._ 2016. Identification of _Klebsiella_ capsule synthesis loci from whole genome data. Microbial Genomics:2(12) DOI: [https://doi.org/10.1099/mgen.0.000102](https://doi.org/10.1099/mgen.0.000102).

If you use the O locus database please cite:

Wick _et al._ 2018. Kaptive Web: User-friendly capsule and lipopolysaccharide serotype prediction for _Klebsiella_ genomes. Journal of Clinical Microbiology:56(6) DOI: [https://doi.org/10.1128/jcm.00197-18](https://doi.org/10.1128/jcm.00197-18)

## Curators

These databases were originally developed by [Kelly Wyres](https://wyreslab.com/research-journey-kelly-wyres/), [Kathryn Holt](https://holtlab.net/) and [Ryan Wick](https://www.doherty.edu.au/staff-member/ryan-wick/), and are now maintained by Kelly Wyres, [Tom Stanton](https://research.monash.edu/en/persons/tom-stanton/) and [Naoise McGarry](https://research.monash.edu/en/persons/naoise-mcgarry/) (Monash University, Australia).

## Contribute

If you think you've found a novel K or O locus please [get in touch](mailto:kaptive.typing@gmail.com) so we can add it to the database (with attribution)!

## License

The databases are distributed under [GNU Genral Public license v3.0](https://github.com/klebgenomics/KpSC_surface_antigen_loci/blob/main/LICENSE). 
