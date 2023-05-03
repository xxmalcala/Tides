# TIdeS

**T**ranscript **Ide**ntification and **S**election (TIdeS) is a method to identify putative open reading frames (pORFs) from a given transcriptome and is able to aid in the bulk decontamination of sequences from "messy" transcriptomic data. Overall, TIdeS couples sequence composition with ML approaches to discern pORFs in the correct reading frame and to identify target sequences from contaminated datasets (e.g. kleptoplastic organisms). 

## Dependencies
+ [Python 3.7+](https://www.python.org/downloads/)
  - [BioPython](https://biopython.org/wiki/Download)
  - [Pandas](https://pandas.pydata.org/)
  - [scikit-learn](https://scikit-learn.org/stable/)
  - [Optuna](https://optuna.org/#installation)
+ [DIAMOND](https://github.com/bbuchfink/diamond)
+ [CD-HIT](https://github.com/weizhongli/cdhit)
+ [Barrnap](https://github.com/tseemann/barrnap)
+ Patience!

## Quick Start

### ORF-Calling and Assessment

**Inputs**
- FASTA formatted transcriptome assembly
- Taxon name (e.g., Homo sapiens, Op_me_Hsap)
- Protein database (can be prepared by "prep_tides_db.sh" in the **util** folder)
```
python3 tides.py --fin <transcriptome-assembly> --taxon <taxon-name> --db <protein-database>
```
#### Arguments
##### Required
```
-f, --fin           Input file in FASTA format
-n, --taxon         Taxon-name or PhyloToL taxon-code
-d, --db            Protien database (FASTA or DIAMOND format)
```
##### Optional
```
-p, --threads       Number of CPU threads (default = 1)
-m, --model         Previously trained TIdeS model (".pkl" file)
-k, --kmer          kmer size for generating sequence features (default = 3)
-q, --quiet         No console output
-ov, --overlap      Permit overlapping kmers (see --kmer)
-gz, --gzip         Tar and gzip TIdeS output
```
#### Example

```cmd
python3 tides.py -f example/TBD -n TBD -d TBD
```


### Decontamination
**Note that these options are currently being streamlined/changed...**
**Inputs**
- FASTA formatted transcriptome assembly
- Taxon name (e.g., Myrionecta rubrum, Sr_ci_Mrub)
- Table of sequence names annotated as 'target' or 'non-target'
```
python3 tides.py --fin <transcriptome-assembly> --taxon <taxon-name> --db <protein-database>
```
Kmer-size and overlap can have dramatic impact on the inference of target/non-target sequences. For contaminated taxa with highly similar composition (e.g. Monocystis agilis [parasite] and Helobdella robusta [host]), recommended to include ```-k 4 -ov``` in the command.
#### Arguments
##### Required
```
-f, --fin           Input file in FASTA format
-n, --taxon         Taxon-name or PhyloToL taxon-code
-c, --contam        Table of sequences annotated as 'target' or 'non-target'
```
##### Optional
```
-p, --threads       Number of CPU threads (default = 1)
-m, --model         Previously trained TIdeS model (".pkl" file)
-k, --kmer          kmer size for generating sequence features (default = 3)
-q, --quiet         No console output
-ov, --overlap      Permit overlapping kmers (see --kmer)
-gz, --gzip         Tar and gzip TIdeS output
```
#### Example

```cmd
python3 tides.py -f example/TBD -n TBD -d TBD -c
```

### Planned Updates - 05-2023
- [ ] Add basic EDS for evaluating contamination
- [ ] Conda and/or PyPi packaging
- [ ] Prepare basic examples (pORF-calls, contamination, EDS for contamination)
