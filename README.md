# BenchmarkingProject_MEMEsuite_HOMER_GimmeMotifs
Bioinformatics Benchmarking project on three motif discovery tools for ATAC-seq and CHIP-seq data.  

# Code
{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "c8b6c7ca-649f-49fd-8326-91a888dbd470",
   "metadata": {},
   "source": [
    "## MOTIF ENRICHMENT/DISCOVERY BENCHMARKING CODE\n",
    "ANGELINA CARCIONE"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f68eafcb-25db-4b30-ae0f-ac70ba6f8248",
   "metadata": {},
   "source": [
    "# TOOL DOWNLOADS\n",
    "MEME Download: https://meme-suite.org/meme/doc/download.html\n",
    "\n",
    "HOMER Download: http://homer.ucsd.edu/homer/download.html\n",
    "\n",
    "GimmeMotifs Download: https://gimmemotifs.readthedocs.io/en/master/installation.html"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a1ad7a3c-d735-46c6-a69c-a9dee46cc3de",
   "metadata": {},
   "source": [
    "# 1 -------------------------------------------------------------\n",
    "# TOY DATA #1\n",
    "Input file: simple_simulated_data.fasta\n",
    "- All of the commands for the 3 softwares are aiming to look for the specific motifs i inputted into 4 different DNA sequences.\n",
    "- the input is the same for all 3\n",
    "- this file has 1 sequence with all 4 motifs in different places\n",
    "\n",
    "True motifs: +MA0108.1, +MA0466.1, +MA0609.1, +MA0080.4\n",
    "- +MA0080.4(SPI1): AAAAAGCGGAAGT\n",
    "- +MA0108.1(TBP): TATAAAAG\n",
    "- +MA0466.1(CEBPB, Basic leucine zipper factors (bZIP)): ATTCGACAAT\n",
    "- +MA0609.1(Crem, Basic leucine zipper factors (bZIP)): ATGACGTAA"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "73eb5b35-c843-48dc-b577-04e1151f1b42",
   "metadata": {},
   "source": [
    "# MEME \n",
    "(formatting: fimo [options][motif file][sequence file], -oc option for output file, motif file must be in meme format)\n",
    "```\n",
    "fimo -oc output_fimo_RANDOM_dna implanted_motifs.meme simple_simulated_data.fasta\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9da01d64-29c4-4ad9-beef-0516544a8a53",
   "metadata": {},
   "source": [
    "# HOMER \n",
    "(formatting: findMotifs.pl[input][promoter set][output directory][options], -find option for scanning (must be a PWM.homer file), fasta to indicate fasta file as input (takes bed by default))\n",
    "```\n",
    "findMotifs.pl -find simple_simulated_data.fasta fasta output_HOMER_RANDOM_dna -find implanted_motifs.homer\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1454b119-b2f8-4a7e-9fdd-ae9c49aec7da",
   "metadata": {},
   "source": [
    "# GimmeMotifs\n",
    "(formatting: gimme scan [input][options], -B for background, -p for PWM in pfm format, -t for table output, > for output)\n",
    "```\n",
    "gimme scan simple_simulated_data.fasta -B background_simple_motifs.fasta -p gimmeMotif_motifs.pfm -t > output_GIMME_RANDOM_dna.txt\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e073d571-8010-4d4f-af31-8b6338dae60b",
   "metadata": {},
   "source": [
    "# 2 -------------------------------------------------------------\n",
    "# TOY DATA #2\n",
    "Input: simple_4_motifs_4_seqs.fasta\n",
    "- All of the compands for the 3 softwares are aiming to look for the specific motifs i inputted into 4 different DNA sequences.\n",
    "- The sequences are the same, but each sequence has a different motif in a different location.\n",
    "- It has 4 motifs, 4 DNA sequences in this file\n",
    "\n",
    "True motifs: +MA0108.1, +MA0466.1, +MA0609.1, +MA0080.4\n",
    "- +MA0080.4: AAAAAGCGGAAGT\n",
    "- +MA0108.1: TATAAAAG\n",
    "- +MA0466.1: ATTCGACAAT\n",
    "- +MA0609.1: ATGACGTAA"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c9a3b031-3c71-4925-bda9-652c7df1f2ee",
   "metadata": {},
   "source": [
    "# MEME\n",
    "(fimo [options][motif file][sequence file], -oc option for output file, --bfile for background file, motif file must be in meme format)\n",
    "```\n",
    "fimo -oc output_4_by_4_meme --bfile meme_background.txt implanted_motifs.meme simple_4_motifs_4_seqs.fasta\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b35ba022-3972-41b6-9400-e86eec881549",
   "metadata": {},
   "source": [
    "# HOMER\n",
    "(formatting: findMotifs.pl[input][promoter set][output directory][options], -find option for scanning (must be a PWM.homer file), fasta to indicate fasta file as input (takes bed by default), -bg option for background file)\n",
    "```\n",
    "findMotifs.pl simple_4_motifs_4_seqs.fasta fasta output_4_by_4_homer -find implanted_motifs.homer -bg background_simple_motifs.fasta\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fcf011e3-fee9-4fbf-826f-015f61397848",
   "metadata": {},
   "source": [
    "# GimmeMotifs\n",
    "(formatting: gimme scan [input][options], -B for background, -p for PWM in pfm format, -t for table output, > for output)\n",
    "```\n",
    "gimme scan simple_4_motifs_4_seqs.fasta -B background_simple_motifs.fasta -p gimmeMotif_motifs.pfm -t > output_4_by_4_gimme.txt\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c5775de3-173b-4475-8f75-90ad7124f01a",
   "metadata": {},
   "source": [
    "# 3 ---------------------------------------------------------------\n",
    "# ChIP-seq Peak Dataset: DATA #3\n",
    "Input: ChIP-seq peak files of VDR in mice\n",
    "- https://academic.oup.com/nar/article/43/W1/W39/2467905#supplementary-data\n",
    "- Case 4 from the meme suite paper, going to do the same as they did (https://pmc.ncbi.nlm.nih.gov/articles/PMC4489269/)\n",
    "- TRUTH: GGGTCATCGGGTTCA or AGGTCACAGAGGTCA aka VDR or vitamin D receptor \n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3298e66b-007a-42d2-b55e-ef600e734272",
   "metadata": {},
   "source": [
    "## FILE PREP for ChIP-seq peak files \n",
    "\n",
    "getting the data from the paper (https://academic.oup.com/nar/article/43/W1/W39/2467905#supplementary-data)\n",
    "```\n",
    "curl -L -o gkv416_Supplementary_Data.zip \"https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/nar/43/W1/10.1093_nar_gkv416/2/gkv416_Supplementary_Data.zip?Expires=1736317153&Signature=fUUq1cAtp1luXiL9FvW6qLfS-YWHx5tQN6Ry1091HxvNW2vErt2LzptHT~MBzYXlSsfGWZSIBmkdpsW9h6pQpZc-8fb~Zq5UiFNSbVqTFpHglqmn1QkQcfaQSf2nA5doNNHHMdOe-MwPMt7wJZAmtDdKWbAKunNHVOWeYcUX9zPn~4L71A6B8EBWZ7pg-uLfrzcxnJ42cnplsHhRdXPPdRarbPFDTYH2cSdadHaSInudAtBk-9gYrtx4mkI0PhMWxfhxHWmeXewDt6eOLesyndMDDvfI~YMPMVGL5pzN77NK9ddJos4RzrgeADQ5LoVAw0UwCkfzpPhl-E4psECh-A__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA\"\n",
    "\n",
    "unzip /home/acarcione/MEME_Supplementary_Data.zip\n",
    "unzip /home/acarcione/nar-00283-web-b-2015-File005.zip\n",
    "```\n",
    "files needed:\n",
    "- inflating: case4/Supplementary_Table_1.500bp.bed\n",
    "- inflating: case4/Supplementary_Table_1.500bp.fa\n",
    "- inflating: case4/Supplementary_Table_1.bed\n",
    "- inflating: case4/Supplementary_Table_1.xls i\n",
    "- in my own folder now: /home/acarcione/case4\n",
    "```\n",
    "cat case4/Supplementary_Table_1.500bp.bed\n",
    "cat case4/Supplementary_Table_1.500bp.fa\n",
    "cat case4/Supplementary_Table_1.bed \n",
    "cat case4/Supplementary_Table_1.xls\n",
    "```\n",
    "this is in the paper\n",
    "```\n",
    "awk '{printf(\"%s\\t%d\\t%d\\n\", $1, (($3 +$2) / 2) - 250, (($3 + $2) + 250))}' case4/Supplementary_Table_1.bed > case4/Supplementary_Table_1.500bp.bed\n",
    "```\n",
    "\n",
    "get Jaspar motifs in MEME format from https://jaspar.elixir.no/downloads/\n",
    "```\n",
    "wget https://jaspar.elixir.no/download/data/2024/CORE/JASPAR2024_CORE_vertebrates_non-redundant_pfms_meme.txt -O Jaspar_vertebrates.meme\n",
    "\n",
    "wget http://thebrain.bwh.harvard.edu/uniprobe/downloads/All/All_PWMs.zip -O all_pwm.meme\n",
    "```\n",
    "\n",
    "need the mouse genome for HOMER and GimmeMotifs since the study was done on mice (genome downloaded from ensembl)\n",
    "```\n",
    "wget https://ftp.ensembl.org/pub/release-113/fasta/mus_musculus/dna/Mus_musculus.GRCm39.dna_sm.toplevel.fa.gz\n",
    "\n",
    "gunzip Mus_musculus.GRCm39.dna_sm.toplevel.fa.gz\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "13d10dc2-f0b3-4f2b-b7db-46b46a9bb9fc",
   "metadata": {},
   "source": [
    "# MEME\n",
    "(formatting: meme-chip [options][primary sequence file], -oc option for output, -dp for PWM databases like JASPAR below)\n",
    "```\n",
    "meme-chip -oc meme_chip_out_withPWM -db /home/acarcione/case4/Jaspar_vertebrates.meme -db /home/acarcione/case4/all_pwm.meme /home/acarcione/case4/Supplementary_Table_1.500bp.fa\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c533d0a0-2856-4d47-8f73-4adf7cb85939",
   "metadata": {},
   "source": [
    "# HOMER\n",
    "(formatting: findMotifs.pl[targetSequences.fa]fasta[output directory][options])\n",
    "```\n",
    "findMotifs.pl /home/acarcione/case4/Supplementary_Table_1.500bp.fa fasta /home/acarcione/ChIP_output_HOMER\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d46883be-1ab2-4afa-8ab0-68cf92fab005",
   "metadata": {},
   "source": [
    "# GimmeMotifs\n",
    "(formatting: gimme motifs [input][output][options], -g option for genome)\n",
    "```\n",
    "gimme motifs /home/acarcione/case4/Supplementary_Table_1.500bp.fa ChIP_output_Gimme -g  Mus_musculus.GRCm39.dna_sm.toplevel.fa\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ea13e6a7-4710-4194-8c1d-4c28dced74c0",
   "metadata": {},
   "source": [
    "# 4 -------------------------------------------------------------\n",
    "# ATAC-Seq peak Dataset: DATA #4\n",
    "Input: ATAC-seq Peak files: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE85853\n",
    "- Paper that produced this data: https://www.cell.com/cancer-cell/fulltext/S1535-6108(17)30204-0\n",
    "- They originally used HOMER\n",
    "- true motifs that were the most \"abundant\" (11 total): NF-κB, Jun-AP1, CTCF, EGR, SMAD, MYC, and KLF, ETS, RUNX, GATA, and STAT\n",
    "- genome: human hg38\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "10453603-438d-4d32-8922-2193881bbc6f",
   "metadata": {},
   "source": [
    "# FILE PREP for ATAC-seq peak data \n",
    "```\n",
    "wget https://ftp.ncbi.nlm.nih.gov/geo/series/GSE85nnn/GSE85853/suppl/GSE85853%5FAllPeaks%2Ebed%2Egz\n",
    "\n",
    "mkdir /home/acarcione/ATAC-seq_peaks\n",
    "\n",
    "gunzip /home/acarcione/GSE85853_AllPeaks.bed.gz > home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.bed\n",
    "```\n",
    "\n",
    "human genome download! (Human genome downloaded from ensembl) \n",
    "```\n",
    "wget https://ftp.ensembl.org/pub/release-113/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz\n",
    "\n",
    "gunzip /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz \n",
    "```\n",
    "\n",
    "Indexing the reference genome using samtools or else it gets mad\n",
    "```\n",
    "samtools faidx /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "head /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "cat /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "```\n",
    "\n",
    "making the bed file into a fasta file since each tool takes it better in my opinion (from what i have gathered while doing this project) \n",
    "```\n",
    "bedtools getfasta -fi /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa -bed /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.bed -fo /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa\n",
    "```\n",
    "\n",
    "something wrong with my bed file: reformatted the chromosome names cause they werent matching with the genome file \n",
    "```\n",
    "bedtools getfasta -fi /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa -bed /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks_no_chr.bed -fo /\n",
    "\n",
    "home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa\n",
    "\n",
    "samtools view -H /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "\n",
    "cat /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.fai\n",
    "\n",
    "awk 'NR==FNR {a[$1]=$2; next} {if ($2 <= a[$1] && $3 <= a[$1]) print $0}' chrom_lengths.txt /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks_no_chr.bed > filtered_bed_file.bed\n",
    "```\n",
    "\n",
    "final bedtools command that puts the peaks in fasta for MEME\n",
    "```\n",
    "bedtools getfasta -fi /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa -bed /home/acarcione/filtered_bed_file.bed -fo /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa\n",
    "\n",
    "head /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9e9f8760-a3ad-493d-8161-0af58a1cb1d5",
   "metadata": {},
   "source": [
    "# MEME\n",
    "formatting: meme-chip [options][primary sequence file], -oc option for output, -dp for PWM databases like JASPAR below, -meme-nmotifs 11 option to search for min 11 motifs)\n",
    "```\n",
    "meme-chip -oc  /home/acarcione/ATAC-seq_peaks/meme_ATAC_out -db /home/acarcione/case4/Jaspar_vertebrates.meme -db /home/acarcione/case4/all_pwm.meme /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa  -meme-nmotifs 11\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6ce1de1e-c57a-4598-a150-5c57478b2eb6",
   "metadata": {},
   "source": [
    "# HOMER \n",
    "(formatting: findMotifs.pl [targetSequences.fa]fasta[output directory][options]) \n",
    "```\n",
    "findMotifs.pl /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa fasta /home/acarcione/ATAC-seq_peaks/ATAC_HOMER_nogenome_output\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "331248ca-7ade-4917-b637-44c52cc50740",
   "metadata": {},
   "source": [
    "# GimmeMotifs\n",
    "(formatting: gimme motifs [input][output][options], -g option for genome)\n",
    "```\n",
    "gimme motifs /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa /home/acarcione/ATAC-seq_peaks/ATAC_GIMME_output -g /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5568bdb4-f7c7-4b65-ad09-d6b443fa825f",
   "metadata": {},
   "source": [
    "# To benchmark time, memory, and CPU usage, I used ```/usr/bin/time --verbose``` for all 4 datasets for each of the commands. \n",
    "output from those results were inputted into R code for plotting histograms for visualization.\n",
    "to benchmark just runtime, command time can be used too."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "edb07817-0d40-42d6-a3cd-be00fa7ddd9a",
   "metadata": {},
   "source": [
    "# Benchmarking memory and time on ChIP-seq DATA\n",
    "```\n",
    "/usr/bin/time --verbose  meme-chip -oc meme_chip_out_withPWM -db /home/acarcione/case4/Jaspar_vertebrates.meme -db /home/acarcione/case4/all_pwm.meme /home/acarcione/case4/Supplementary_Table_1.500bp.fa\n",
    "\n",
    "/usr/bin/time --verbose  gimme motifs /home/acarcione/case4/Supplementary_Table_1.500bp.fa ChIP_output_Gimme -g  Mus_musculus.GRCm39.dna_sm.toplevel.fa\n",
    "\n",
    "/usr/bin/time --verbose  findMotifs.pl /home/acarcione/case4/Supplementary_Table_1.500bp.fa fasta /home/acarcione/ChIP_output_HOMER\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8102b907-267a-4d9c-ad02-dd7e24f6d25a",
   "metadata": {},
   "source": [
    "# Benchmarking memory and time on ATAC-seq DATA\n",
    "```\n",
    "/usr/bin/time --verbose meme-chip -oc  /home/acarcione/ATAC-seq_peaks/meme_ATAC_out -db /home/acarcione/case4/Jaspar_vertebrates.meme -db /home/acarcione/case4/all_pwm.meme /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa  -meme-nmotifs 11 \n",
    "\n",
    "/usr/bin/time --verbose findMotifs.pl /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa fasta /home/acarcione/ATAC-seq_peaks/ATAC_GIMME_output -fastaBg /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "\n",
    "/usr/bin/time --verbose gimme motifs /home/acarcione/ATAC-seq_peaks/ATAC-seq_peaks.fa /home/acarcione/ATAC-seq_peaks/ATAC_GIMME_output -g /home/acarcione/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa\n",
    "```\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8b9026eb-d31e-499e-8962-276817ac066b",
   "metadata": {},
   "source": [
    "# Plotting time and memory for Toy 1, Toy 2, ChIP-seq, and ATAC-seq using R language\n",
    "All time and memory data from ```/usr/bin/time --verbose ``` command output\n",
    "Used packages ggplot and tidyr https://r-graph-gallery.com/220-basic-ggplot2-histogram.html"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d13bbd6c-264c-4fa0-8318-366ad29b10be",
   "metadata": {},
   "source": [
    "# MEMORY USAGE FOR Toy 1 DATA\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2) \n",
    "#you need ggplot2 to plot histograms \n",
    "\n",
    "# create a data frame to store memory data in kb\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  Memory = c(5340, 241208, 10588)\n",
    ")\n",
    "\n",
    "# defining the colors for each tool seperately \n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "# creating the bar plot using the time_data data frame made, aes for aesthetics, xaxis tools, yaxis memory \n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = Memory, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Memory Usage by Motif Enrichment Tools for Toy 1 Data\", \n",
    "       x = \"Tool\", y = \"Memory (in KB)\")\n",
    "\n",
    "# geom_bar to make the bar plot, and based on the identity. \n",
    "\n",
    "# scale_fill_manual adds my colors \n",
    "\n",
    "# theme minimal for minimalistic plot\n",
    "\n",
    "# labs for labels for title, x, and y axis \n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8ef99fea-6d4a-418f-89f7-fdd4404a0c63",
   "metadata": {},
   "source": [
    "# EXECUTION TIME FOR Toy 1 DATA\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "install.packages(\"tidyr\")\n",
    "library(ggplot2)\n",
    "\n",
    "# create a data frame to store time data in seconds \n",
    "\n",
    "\n",
    "#have to convert mins and seconds to just seconds\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"HOMER\", \"MEME-ChIP\", \"GimmeMotifs\"),\n",
    "  Real = c(00.15, 00.13, 05.13),\n",
    "  User = c(0.07, 0.13, 11.02),\n",
    "  Sys = c(0.02, 0.00, 3.14)\n",
    ")\n",
    "\n",
    "\n",
    "library(tidyr)\n",
    "\n",
    "# tidyr to use pivot longer so dataframe reshaped \n",
    "\n",
    "#https://tidyr.tidyverse.org/articles/pivot.html\n",
    "\n",
    "time_fixed <- pivot_longer(time_data,\n",
    "                          cols = c(Real, User, Sys),\n",
    "                          names_to = \"Type\",\n",
    "                          values_to = \"Time\")\n",
    "\n",
    "# creating the bar plot using the time_data data frame made, aes for aesthetics, xaxis tools, yaxis memory \n",
    "\n",
    "p <- ggplot(time_fixed, aes(x = Tool, y = Time, fill = Type)) + \n",
    "  geom_bar(stat = \"identity\", position = \"dodge\") + \n",
    "  scale_fill_manual(values = c(\"Real\" = \"blue\", \n",
    "                               \"User\" = \"green\", \n",
    "                               \"Sys\" = \"coral\")) +\n",
    "  theme_minimal() + \n",
    "  labs(title = \"Execution Times for Motif Enrichment Tools for Toy 1 Data\", \n",
    "       x = \"Tool\", \n",
    "       y = \"Time (seconds)\") +\n",
    "  theme(axis.text.x = element_text(angle = 45, hjust = 1))\n",
    "\n",
    "# geom_bar to make the bar plot, and based on the identity. \n",
    "\n",
    "# scale_fill_manual adds my colors \n",
    "\n",
    "# theme minimal for minimalistic plot\n",
    "\n",
    "# labs for labels for title, x, and y axis\n",
    "\n",
    "# axis text makes the names at an angle so they fit better (45 degrees) \n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fa90db36-914b-49d2-ae67-f36f7d8ec711",
   "metadata": {},
   "source": [
    "# CPU USAGE FOR Toy 1 DATA\n",
    "```\n",
    "# https://r-graph-gallery.com/220-basic-ggplot2-histogram.html\n",
    "\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "# you need ggplot2 to plot histograms \n",
    "\n",
    "# create a data frame to store memory data in kb\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  CPU_use = c(99, 275, 66)\n",
    ")\n",
    "\n",
    "# defining the colors for each tool seperately \n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "# creating the bar plot using the time_data data frame made, aes for aesthetics, xaxis tools, yaxis memory\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = CPU_use, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Percent CPU given to Motif Enrichment Tools for Toy 1 Data\", \n",
    "       x = \"Tool\", y = \"% of CPU\")\n",
    "\n",
    "\n",
    "# geom_bar to make the bar plot, and based on the identity. \n",
    "\n",
    "# scale_fill_manual adds my colors \n",
    "\n",
    "# theme minimal for minimalistic plot\n",
    "\n",
    "# labs for labels for title, x, and y axis\n",
    "\n",
    "print(p)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "124ef2a3-be91-47a6-813a-1f8abf0cb393",
   "metadata": {},
   "source": [
    "# MEMORY USAGE FOR Toy 2 DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  Memory = c(5212, 241512, 10564)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = Memory, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Memory Usage by Motif Enrichment Tools for Toy 2 Data\", \n",
    "       x = \"Tool\", y = \"Memory (in KB)\")\n",
    "\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b6bdf232-1149-4c75-85d4-d934db6f790b",
   "metadata": {},
   "source": [
    "# EXECUTION TIME FOR Toy 2 DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "install.packages(\"tidyr\")\n",
    "library(ggplot2)\n",
    "\n",
    "# have to convert mins and seconds to just seconds\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"HOMER\", \"MEME-ChIP\", \"GimmeMotifs\"),\n",
    "  Real = c(00.15, 00.29, 04.83),\n",
    "  User = c(0.10, 0.21, 10.33),\n",
    "  Sys = c(0.02, 0, 3.14)\n",
    ")\n",
    "\n",
    "library(tidyr)\n",
    "# https://tidyr.tidyverse.org/articles/pivot.html\n",
    "time_fixed <- pivot_longer(time_data,\n",
    "                          cols = c(Real, User, Sys),\n",
    "                          names_to = \"Type\",\n",
    "                          values_to = \"Time\")\n",
    "\n",
    "p <- ggplot(time_fixed, aes(x = Tool, y = Time, fill = Type)) + \n",
    "  geom_bar(stat = \"identity\", position = \"dodge\") + \n",
    "  scale_fill_manual(values = c(\"Real\" = \"blue\", \n",
    "                               \"User\" = \"green\", \n",
    "                               \"Sys\" = \"coral\")) +\n",
    "  theme_minimal() + \n",
    "  labs(title = \"Execution Times for Motif Enrichment Tools for Toy 2 Data\", \n",
    "       x = \"Tool\", \n",
    "       y = \"Time (seconds)\") +\n",
    "  theme(axis.text.x = element_text(angle = 45, hjust = 1))\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0fcda525-2eee-42c8-8877-27d59cf4dbd4",
   "metadata": {},
   "source": [
    "# CPU USAGE FOR Toy 2 DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "# https://r-graph-gallery.com/220-basic-ggplot2-histogram.html\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  CPU_use = c(73, 284, 81)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = CPU_use, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Percent CPU given to Motif Enrichment Tools for Toy 2 Data\", \n",
    "       x = \"Tool\", y = \"% of CPU\")\n",
    "\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f5c31501-99e4-498e-93bb-c8dd5329f49f",
   "metadata": {},
   "source": [
    "# MEMORY USAGE FOR CHIP-SEQ DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  Memory = c(315648, 5356256, 885876)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = Memory, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Memory Usage by Motif Enrichment Tools for ChIP-seq Data\", \n",
    "       x = \"Tool\", y = \"Memory (in KB)\")\n",
    "\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "607481b0-4d92-4738-8669-d917e9cd9300",
   "metadata": {},
   "source": [
    "# EXECUTION TIME FOR CHIP-SEQ DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "install.packages(\"tidyr\")\n",
    "library(ggplot2)\n",
    "\n",
    "# have to convert mins and seconds to just seconds\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"HOMER\", \"MEME-ChIP\", \"GimmeMotifs\"),\n",
    "  Real = c(1378.615, 1177.717, 3788.091),\n",
    "  User = c(1372.496, 1174.587, 9644.645),\n",
    "  Sys = c(4.91, 1.839, 848.54)\n",
    ")\n",
    "\n",
    "library(tidyr)\n",
    "# https://tidyr.tidyverse.org/articles/pivot.html\n",
    "time_fixed <- pivot_longer(time_data,\n",
    "                          cols = c(Real, User, Sys),\n",
    "                          names_to = \"Type\",\n",
    "                          values_to = \"Time\")\n",
    "\n",
    "p <- ggplot(time_fixed, aes(x = Tool, y = Time, fill = Type)) + \n",
    "  geom_bar(stat = \"identity\", position = \"dodge\") + \n",
    "  scale_fill_manual(values = c(\"Real\" = \"blue\", \n",
    "                               \"User\" = \"green\", \n",
    "                               \"Sys\" = \"coral\")) +\n",
    "  theme_minimal() + \n",
    "  labs(title = \"Execution Times for Motif Enrichment Tools\", \n",
    "       x = \"Tool\", \n",
    "       y = \"Time (seconds)\") +\n",
    "  theme(axis.text.x = element_text(angle = 45, hjust = 1))\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c1095fa3-acb2-4707-9469-12011227c680",
   "metadata": {},
   "source": [
    "# CPU USAGE FOR CHIP-SEQ DATA (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "# https://r-graph-gallery.com/220-basic-ggplot2-histogram.html\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  CPU_use = c(99, 294, 99)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = CPU_use, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Percent CPU given to Motif Enrichment Tools for ChIP-seq Data\", \n",
    "       x = \"Tool\", y = \"% of CPU\")\n",
    "\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "aaadee46-c876-474f-be08-13d5bd0c151c",
   "metadata": {},
   "source": [
    "# MEMORY USAGE FOR ATAC-SEQ DATA (same code different numbers) (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  Memory = c(7.263916, 7.249544, 2.386432)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = Memory, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Memory Usage by Motif Enrichment Tools for ATAC-seq Data\", \n",
    "       x = \"Tool\", y = \"Memory (in GB)\")\n",
    "\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "03fc9598-be6d-42f7-a699-b83183544a1b",
   "metadata": {},
   "source": [
    "# EXECUTION TIME FOR ATAC-SEQ DATA (same code, different data/numbers) (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "install.packages(\"ggplot2\")\n",
    "install.packages(\"tidyr\")\n",
    "library(ggplot2)\n",
    "\n",
    "# have to convert mins and seconds to just seconds\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"HOMER\", \"MEME-ChIP\", \"GimmeMotifs\"),\n",
    "  Real = c(16925, 32424, 55198),\n",
    "  User = c(16804.82, 25544.10, 390267.19),\n",
    "  Sys = c(108.44, 393.99, 780.19)\n",
    ")\n",
    "\n",
    "library(tidyr)\n",
    "# https://tidyr.tidyverse.org/articles/pivot.html\n",
    "time_fixed <- pivot_longer(time_data,\n",
    "                          cols = c(Real, User, Sys),\n",
    "                          names_to = \"Type\",\n",
    "                          values_to = \"Time\")\n",
    "\n",
    "p <- ggplot(time_fixed, aes(x = Tool, y = Time, fill = Type)) + \n",
    "  geom_bar(stat = \"identity\", position = \"dodge\") + \n",
    "  scale_fill_manual(values = c(\"Real\" = \"blue\", \n",
    "                               \"User\" = \"green\", \n",
    "                               \"Sys\" = \"coral\")) +\n",
    "  theme_minimal() + \n",
    "  labs(title = \"Execution Times for Motif Enrichment Tools for ATAC-seq DATA\", \n",
    "       x = \"Tool\", \n",
    "       y = \"Time (seconds)\") +\n",
    "  theme(axis.text.x = element_text(angle = 45, hjust = 1))\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ea9d044c-c41d-404b-ac65-a4bd2a577b12",
   "metadata": {},
   "source": [
    "# CPU USAGE FOR ATAC-SEQ DATA (same code, different data/numbers) (for more in-depth comments see toy 1 code)\n",
    "```\n",
    "# https://r-graph-gallery.com/220-basic-ggplot2-histogram.html\n",
    "install.packages(\"ggplot2\")\n",
    "library(ggplot2)\n",
    "\n",
    "time_data <- data.frame(\n",
    "  Tool = c(\"MEME\", \"GimmeMotifs\", \"HOMER\"),\n",
    "  CPU_use = c(99, 708, 99)\n",
    ")\n",
    "\n",
    "colors <- c(\"MEME\" = \"lightblue\", \"HOMER\" = \"lightgreen\", \"GimmeMotifs\" = \"purple\")\n",
    "\n",
    "p <- ggplot(time_data, aes(x = Tool, y = CPU_use, fill = Tool)) + \n",
    "  geom_bar(stat = \"identity\") + \n",
    "  scale_fill_manual(values = colors) + \n",
    "  theme_minimal() + \n",
    "  labs(title = \"Percent CPU given to Motif Enrichment Tools for ATAC-seq Data\", \n",
    "       x = \"Tool\", y = \"% of CPU\")\n",
    "\n",
    "print(p)\n",
    "```"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2e6f0db0-bea3-40c2-9938-48106c3e81d5",
   "metadata": {},
   "source": [
    "# Table for accuracy calulations\n",
    "Calculations done by hand in word \n",
    "\n",
    "Sensitivity (recall) = true positive / (true positive + false negative) \n",
    "\n",
    "Precision = true positive / (true positive + false positive) "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b4823040-5440-4845-9b91-688bdc2a8d05",
   "metadata": {},
   "source": [
    "# Designing the simulated data for Toy 1 and Toy 2 data\n",
    "All my sequences were randomly generated using a random DNA sequence generator (https://faculty.ucr.edu/~mmaduro/random.htm).\n",
    "\n",
    "I then transferred those over to Geneious Prime, a tool I have access to thanks to my lab. \n",
    "\n",
    "For the 1 sequence, 4 motifs file, I picked a random location in the sequence and pasted the motifs in. For the 4 sequences, 1 motif per sequence (each a different motif), I gave them all a motif at the 5,000 bp region. \n",
    "\n",
    "Geneious Zip File with all my simulated data: https://1drv.ms/u/c/a08d5de35af36ea8/ESR5Gm_h7f1Om1lX1ZvrybIB0lZH3kWuI1q34n3Wb7QVRw?e=Do76Ag\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3a3c8d5b-cb5f-4fbe-bec0-f57898642f25",
   "metadata": {},
   "source": [
    "# Links for all documentation for tools used \n",
    "GimmeMotifs Documentation: https://gimmemotifs.readthedocs.io/en/master/reference.html#command-gimme-motifs\n",
    "\n",
    "FIMO Documentation: https://web.mit.edu/meme_v4.11.4/share/doc/fimo.html\n",
    "\n",
    "MEME-ChIP documentation: https://meme-suite.org/meme/doc/meme-chip.html\n",
    "\n",
    "HOMER documentation: http://homer.ucsd.edu/homer/\n",
    "\n",
    "GimmeMotifs Github: https://github.com/vanheeringen-lab/gimmemotifs/tree/master\n",
    "\n",
    "ATAC-seq Peak files: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE85853\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
