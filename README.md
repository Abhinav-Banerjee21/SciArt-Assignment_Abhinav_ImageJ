# ImageJ Particle Counting Protocol

**Assignment 1 – Image Analysis**

## Step 0: Image Acquisition

I first downloaded a raw fluorescence microscopy image from an online database (OpenCell/ImageJ sample datasets). I made sure that the particles in the image were clearly distinguishable from the background and that the image was not pre-processed.

The original image was saved in the `data/raw/` folder without modification. I also recorded the metadata of the image, including source, magnification, pixel size (if available), and staining/channel information, in a separate metadata file.

---

## Step 1: Opening and Pre-processing the Image

I opened the image in ImageJ using:
File → Open

To standardize the format, I converted the image to 8-bit grayscale:
Image → Type → 8-bit

Next, I removed background noise using the subtract background function:
Process → Subtract Background

* Rolling Ball Radius used: **12 pixels**
* Light background option: **Not selected**

This step helped in reducing uneven illumination and improving particle visibility.

After that, I adjusted the brightness and contrast:
Image → Adjust → Brightness/Contrast

I first applied Auto, and then manually fine-tuned the levels to make the particles more clearly visible without overexposing the image.

---

## Step 2: Thresholding

To separate particles from the background, I applied thresholding:
Image → Adjust → Threshold

* Method used: **Default**
* Lower threshold value: **217**
* Upper threshold value: **255**
* Display mode: **Black & White**

I adjusted the threshold sliders until the particles appeared clearly highlighted while minimizing background noise.

After achieving a satisfactory selection, I applied the threshold to convert the image into a binary format.

Since some particles were touching or clustered, I applied watershed segmentation:
Process → Binary → Watershed

This helped in separating overlapping particles by introducing 1 pixel boundaries between them.

---

## Step 3: Setting Measurements

Since the image did not contain a scale bar, I performed all measurements in pixel units.

I then selected the parameters required for analysis:
Analyze → Set Measurements

The following measurements were selected:

* Area
* Perimeter
* Feret’s Diameter
* Shape Descriptors
* Mean Gray Value

---

## Step 4: Particle Analysis

I performed particle analysis using:
Analyze → Analyze Particles

The parameters used were:

* Size range: **50 – Infinity pixels²**
* Circularity: **0.4 – 1.0**

These values were chosen to exclude very small noise particles and focus on roughly circular objects.

The following options were enabled:

* Display Results
* Summarize
* Exclude on Edges
* Add to Manager
* Overlay

After running the analysis, a results table was generated along with an overlay showing detected particles.

---

## Step 5: Saving and Exporting Results

The results table was saved as a CSV file:
Results → File → Save As

Saved in:
`results/stats/particle_count_results.csv`

Next, I flattened the overlay to permanently embed the particle outlines on the image:
Image → Overlay → Flatten

The processed image was then saved as a TIFF file:
File → Save As → TIFF

Saved in:
`data/processed/particle_analysis_annotated.tif`

Since no scale calibration was performed, no scale bar was added to the final image.

---

## Final Outcome

At the end of the analysis, I obtained:

* A CSV file containing quantitative measurements of all detected particles
* An annotated image with clearly marked particle boundaries

This protocol ensures reproducible particle detection and analysis in ImageJ, with parameter selection tailored to the specific image.

-----------------------------------------------------------------------------------------------------------------------------










# BioRender Protocol: High-Efficiency Selection-Free Gene Knock-in via iCRISPR

**Author:** Abhinav Banerjee  
**Institution:** Institute of Bioinformatics and Biotechnology (IBB), SPPU  
**Reference:** Verma, N., et al. (2017). *CRISPR/Cas-mediated knockin in human pluripotent stem cells*. Methods in Molecular Biology.

## 📌 Project Overview
This document outlines the step-by-step BioRender construction protocol for visualizing the "iCRISPR" genome editing methodology. Unlike traditional CRISPR workflows that require external delivery of the Cas9 protein via electroporation, this infographic maps a highly efficient, selection-free protocol using a Doxycycline-inducible Cas9 system combined with liposomal transfection. 

**Canvas Specifications:**
* **Tool:** [BioRender](https://biorender.com/)
* **Dimensions:** 1200 x 628 px (Horizontal Layout)
* **Design Rule:** A single `Human Stem Cell` icon is used across Zones 1, 2, and 4 to ensure visual continuity of the same cell line undergoing sequential modifications.

---

## 🛠️ Step-by-Step Construction Guide

### ZONE 1: ACTIVATION (Dox-mediated Cas9 Expression)
* **Concept:** Activating the integrated "sleeper" Cas9 gene within the hPSC genome.
* **BioRender Elements:** `Human Stem Cell`, `Nucleus`, `Double Helix`, `Genetic Element` (x2), `Small Molecule`, `Cas9 Protein`.
* **Instructions:**
  1. Place the `Human Stem Cell` icon on the far left. 
  2. Inside the nucleus, place a `Double Helix` topped with two `Genetic Element` blocks labeled **TRE** and **Cas9**.
  3. Place a `Small Molecule` icon outside the cell labeled **Doxycycline (DOX)**. 
  4. Draw a dashed arrow from the DOX molecule to the TRE promoter.
  5. Place 2–3 `Cas9` protein icons in the cytoplasm to represent successful endogenous expression.

### ZONE 2: DELIVERY (Liposomal Transfection)
* **Concept:** Chemical delivery of the editing payload (gRNA and Donor DNA) into the Cas9-primed cell.
* **BioRender Elements:** `Liposome`, `sgRNA`, `Circular Plasmid` (or `ssDNA`), identical `Human Stem Cell` (from Zone 1).
* **Instructions:**
  1. Group an `sgRNA` icon and a `Donor Template` icon inside a `Liposome` vehicle.
  2. Position the loaded Liposome so it overlaps the outer membrane of the cell, illustrating endocytosis/membrane fusion.
  3. Ensure the `Cas9` proteins generated in Zone 1 are still visible in the cytoplasm.
  4. Draw a faded motion path showing the sgRNA and Donor DNA escaping the liposome and moving toward the nucleus.

### ZONE 3: MECHANISM (Targeted DSB & HDR Repair)
* **Concept:** The molecular cut-and-paste utilizing the cell's homology-directed repair machinery.
* **BioRender Elements:** `Cas9 RNP`, `Double Stranded DNA`, `DNA Double Strand Break`, `Scissors`.
* **Instructions:**
  1. **RNP Assembly:** Stack a `Cas9 RNP` icon directly on top of a straight `Double Stranded DNA` helix. 
  2. **Cleavage:** Below this, place the `DNA Double Strand Break` icon with a `Scissors` icon hovering over the gap.
  3. **Repair:** At the bottom, place a final DNA helix. Use the BioRender shape tool to insert a distinctly colored rectangle (e.g., Neon Green) into the gap. 
  4. Draw dashed lines (Homology Arms) connecting the exogenous Donor Template to the edges of the genomic insertion site.

### ZONE 4: VALIDATION (Selection-Free Genotyping)
* **Concept:** Confirming successful knock-in without the use of antibiotic selection markers.
* **BioRender Elements:** `96-well plate`, `Agarose Gel`, `Human Stem Cell` (with glow effect).
* **Instructions:**
  1. Draw a sweeping transition arrow from the Zone 3 nucleus to a `96-well plate`. Highlight 2-3 specific wells in the same color as your Zone 3 insert to represent positive clones.
  2. Next to the plate, add an `Agarose Gel` icon. Draw two distinct bands:
     * **Lane 1 (WT):** A lower white band representing the wild-type locus.
     * **Lane 2 (KI):** A higher white band representing the heavier, successfully edited Knock-in locus (Band-shift analysis).
  3. Conclude with the final `Human Stem Cell` icon. Apply an outer glow effect matching the insert color to signify stable expression of the target reporter/tag.

---

## 🎨 Design & Formatting Rules
To ensure the infographic is conference-ready, adhere to the following constraints:
1. **Color Consistency:** The color chosen for the Donor Insert (Zone 2) must perfectly match the integrated sequence (Zone 3), the positive wells (Zone 4), and the final cell glow (Zone 4).
2. **Typography:** Use sans-serif fonts (e.g., Arial, Helvetica) uniformly. Main titles at 18-24pt, zone headers at 14pt, and detailed annotations at 10-12pt.
3. **Alignment:** Use BioRender's alignment tools to ensure all horizontal DNA helices in Zone 3 share the same X-axis, and all zone headers are aligned to the top.

