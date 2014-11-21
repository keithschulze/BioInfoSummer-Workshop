# Counting cells

## Aim
Count the number of cells in an image

<p>1. Open image "[...]/images/Widefield/Cell Segmentation/Nuclei.tif"</p>
<p>2. Segment by thresholding:</p>

```
Image → Adjust → Threshold
Li auto-thresholding method
```

Some nuclei are touching one another. Obviously this will skew the results; however, the "Watershed" binary morphology filter is able to split touching objects. It works particularly well for ellipsoid shapes.

<p>3. Split touching cell using watershed.</p>

`Process → Binary → Watershed`

<p>4. Use connected components (or Particle Analysis in the ImageJ world) to count number of cells and extract cellular parameters.</p>

`Analyze →  Analyze Particles...`

![](../images/demo2/analyze_particles.png)

Note: Filtering the output is really useful. For instance, setting a small size filter can help to exclude tiny speckles that might arise from noise derived 'bright' pixels that make the threshold.


![Results](../images/demo2/results.png)


![Summary results](../images/demo2/summary.png)

