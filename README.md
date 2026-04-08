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



