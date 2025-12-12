# End-to-End-Genomics-DeepSEA-XAI-Pipeline
Integrative Framework for NGS Variant Discovery and Deep Learning Based Functional Prioritization with Explainable AI XAI
# Integrative Framework for NGS Variant Discovery and Deep Learning-Based Functional Prioritization with Explainable AI (XAI)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Bioinformatics](https://img.shields.io/badge/Bioinformatics-NGS-green)
![Deep Learning](https://img.shields.io/badge/AI-DeepSEA%2FKipoi-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## 📌 Project Overview
This repository contains an end-to-end bioinformatics pipeline designed to identify genetic variants from raw Next-Generation Sequencing (NGS) data and predict their functional impact using Deep Learning.

Unlike standard pipelines that stop at variant calling, this framework integrates **DeepSEA** (via the Kipoi model zoo) to score non-coding regulatory variants and applies **Explainable AI (XAI)** techniques (In-Silico Saturation Mutagenesis) to interpret *why* specific mutations are flagged as high-impact.

The pipeline spans **16 modular steps**, covering alignment, variant calling, clinical annotation, pathway enrichment, and visual verification.

---

## 🏗️ Architecture & Workflow

The pipeline follows a linear, modular architecture:

1.  **Read Mapping:** Alignment of raw reads to hg38 using `BWA-MEM`.
2.  **Variant Discovery:** Identification of SNPs/Indels using `Bcftools`.
3.  **AI Prediction:** Functional impact scoring using the **DeepSEA** neural network.
4.  **Clinical Annotation:** Gene mapping and ClinVar/dbSNP lookup via `MyVariant`.
5.  **Systems Biology:** Pathway enrichment analysis (KEGG/Reactome) using `GSEApy`.
6.  **Visual Verification:** Automated generation of read pileup plots for top hits.
7.  **Explainability (XAI):** In-silico mutagenesis heatmaps to visualize decision boundaries.

---

## 🛠️ Prerequisites & Installation

The pipeline is designed to run in **Google Colab** or a Linux-based environment (Ubuntu 20.04+).

### System Dependencies
The following tools are installed automatically by the pipeline scripts:
* `bwa` (Burrows-Wheeler Aligner)
* `samtools` & `bcftools`
* `bedtools`
* `libhdf5-dev` (for H5PY compatibility)

### Python Libraries
Key Python packages used:
* `kipoi`, `kipoiseq` (Deep Learning Genomics)
* `pysam` (BAM/FASTA handling)
* `myvariant` (Clinical Annotation)
* `gseapy` (Pathway Analysis)
* `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly` (Data Science & Viz)

---

## 🚀 Usage

The pipeline is divided into 16 sequential steps. 

### Phase 1: NGS Data Processing
* **Step 1-3:** Environment setup and raw data retrieval (SRA/FASTQ).
* **Step 4:** Reference Genome Indexing (hg38/chr22).
* **Step 5:** Read Alignment (`bwa mem`).
* **Step 6:** BAM Conversion & Sorting (`samtools`).
* **Step 7:** Variant Calling (`bcftools mpileup`).

### Phase 2: Deep Learning & Annotation
* **Step 8:** **Functional Prediction.** Runs the DeepSEA model to predict chromatin effects.
* **Step 9:** **Visualization.** Generates genome-wide impact plots (Scatter/Histogram).
* **Step 11:** **Clinical Annotation.** Queries ClinVar and dbSNP.
* **Step 12:** **Motif Analysis.** Hypothesizes transcription factor disruption.

### Phase 3: Validation & Explainability
* **Step 13:** **Visual Proof.** Generates a pileup snapshot of the top variant to verify read support.
* **Step 14:** **Pathway Enrichment.** Checks for over-represented biological pathways (e.g., Immune System).
* **Step 15:** **XAI Analysis.** Performs In-Silico Saturation Mutagenesis to generate a sensitivity heatmap.
* **Step 16:** **Master Archive.** Zips and downloads all outputs.

---

## 📊 Outputs

Upon completion, the pipeline generates a `Complete_Bioinformatics_Pipeline.zip` containing:

| File Name | Description |
| :--- | :--- |
| `variants.vcf` | Raw list of genetic variants found in the sample. |
| `deepsea_results.csv` | Variants annotated with DeepSEA functional impact scores. |
| `deepsea_annotated_clinical.csv` | The "Golden Dataset" merging AI scores with gene names and rsIDs. |
| `DeepSEA_Interactive_Map.html` | Interactive genome browser plot (Zoomable). |
| `Top_Variant_Pileup.png` | Visual verification of the sequencing reads at the top site. |
| `DeepSEA_XAI_Heatmap.png` | AI Explainability heatmap showing mutation sensitivity. |

---

## 🔬 Key Findings (Example)
* **Top Candidate:** Variant `rs1217596845` at `chr22:10580500` (C>T).
* **AI Score:** **0.28** (Predicted High Impact on Chromatin).
* **Biological Context:** Non-coding regulatory variant with no prior gene annotation (Novel), flagged by DeepSEA as functionally significant.

---

## 📜 Acknowledgements
* **DeepSEA:** Zhou, J., & Troyanskaya, O. G. (2015). Predicting effects of noncoding variants with deep learning. *Nature Methods*.
* **Kipoi:** The Kipoi Model Zoo for Genomics.
* **MyVariant.info:** High-performance variant query API.

---

## 📝 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
