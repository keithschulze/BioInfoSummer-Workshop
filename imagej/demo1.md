# Fluorescent stain measurement
Fluorescent wide field images of three fluorescent markers/stains:

* Blue: DAPI nuclear marker
* Red: Marker for wounding
* Green: Cytoplasmic marker for healthy cells.

![](../images/demo1/fluoro_01_crop.png)

---

**Aim:**
Analyse the area covered and/or intensity of marker for wounding. 

1. Open "[...]/Images/Widefield/Fluorescence Measurement/Fluoro 01.tif" 

2. Calibrate the image:

```
Image → Properties
Unit of length: µm
Pixel width: 0.6
Pixel height: 0.6
Voxel depth: 1
```

Calibration are usually encoded in the image metadata in modern microscopes; however, we need to use calibration images for older microscopes. 

<p>3. Split channels so we can do measurements on a specific channel.</p>

`Image → Colour → Split Channels`

![](../images/demo1/fluoro_01_crop_red.png)

---

## Filtering

<p>4. Apply a Gaussian Blur with a sigma of 1 px to reduce noise.</p>

`Process → Filters → Gaussian Blur...`

A Gaussian blur filter helps to smooth noise that is typically present in images acquired with highly sensitive cameras.

![](../images/demo1/fluoro_01_blur.png)

---

## Segmentation

<p>5. Threshold based segmentation:</p>

`Image → Adjust → Threshold...`

![](../images/demo1/threshold.png)

Thresholding segments the images based on pixel intensity. Thresholds can be set manually or automatically via algorithms that examine the image histogram.

![](../images/demo1/fluoro_01_crop_red_blur_bin.png)

---

## Measurement

<p>6. Set measurement types:</p>

```
Analyze → Set Measurements...
Tick: Area, Min & max grey value, Mean grey value, Area Fraction, Limit to Threshold, Display label 
```

![](../images/demo1/set_measurements.png)


<p>7. Measure:</p>

` Analyze → Measure`

Here measurement is determining the cumulative area of all stained parts. Later we will utilise connected components to analysis individual characteristics.

![](../images/demo1/fluoro_measure_result.png)

