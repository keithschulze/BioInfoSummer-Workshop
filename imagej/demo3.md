# Cell scoring
Extension of the previous demo. Widefield fluorescent images where cells are expressing markers for proliferation (green) and death (red).

Markers:

- Blue - DAPI Nuclear marker.
- Green - Ki67 cell proliferation marker.
- Red - Ph3 cell death marker.

![](../images/demo3/cell_score.png)

## Aim
Determine the proportion of total cells that express different markers.

<p>1. Open image: "[...]/Images/Widefield/Cell Scoring and Cycle/Control.tif"</p>


<p>2. Split the channels so we can work on them individually</p>

`Image → Color → Split Channels`

![](../images/demo3/cell_score_split.png)


## Determine total cell number

<p>3. Segment the DAPI (blue) channel by thresholding.</p>

```
Image → Adjust → Threshold...
Select "Li" AutoThreshold method.
```

<p>4. Split touching cells with a Watershed binary morphological filter.</p>

`Process → Binary → Watershed`

![](../images/demo3/cell_score_c3_bin_vs_ws.png)

<p>5. Use connected components (or Particle Analysis in the ImageJ world) to count number of cells. We set a minimum size filter in order to discard any small dots derived from noise that surpass the threshold segmentation.</p>

`Analyze → Analyze Particles...`

![](../images/demo3/analyze_parts.png)

![](../images/demo3/total_cell_number.png)

## Crude approach to determine the number of cells expressing the Ki67 cell proliferation and Ph3 cell death markers

We could use a similar approach to that used for total cell number except that we don't need to use the watershed morphological filter to split cells.

<p>6. Segment the Ki67 (green) and Ph3 (red) channel by thresholding.</p>

```
Image → Adjust → Threshold...
Select "Li" AutoThreshold method.
```

![](../images/demo3/cell_score_c1_c2_bin.png)

<p>7. Particle analysis to count number of cells.</p>

`Analyze → Analyze Particles...`

![](../images/demo3/results.png)


## Improving precision
This process works reasonably for the two markers; however, our lower size cutoff does exclude some of red expressing cells because the marker isn't expressed strongly or throughout the entire nuclei and thus doesn't make the size cutoff. More generally, it is often the case that some markers such as a DAPI marker are simply more reliable, hence it would be nice if we could use the DAPI segmentation as a 'template' to find to find cell that express other markers.

Geodesic reconstruction can do exactly this. We will make use of the third-party [MorphoLib](https://github.com/ijpb/MorphoLibJ) plugin for morphological operators.

<p>8. Run the Geodesic Reconstruction plugin using each segmented marker image(i.e., binary images for Ki67 and Ph3) and the segmented DAPI image as the mask.</p>

![](../images/demo3/geodesic_recon.png)

![](../images/demo3/cell_score_c1_c2_c3_bin_gr.png)

<p>7. Particle analysis to count number of cells in the reconstucted images.</p>

`Analyze → Analyze Particles...`

![](../images/demo3/results_gr.png)

