# Refinements
Total cell number and number of cells expressing markers are determined independently on each image. However, the number of cells expressing a specific marker cannot be reliably determined from those the marker channel images because marker expression is variable and is not homogenous across nuclei like DAPI.

Geodesic reconstruction allows us to use a reliable marker like DAPI to determine which cells overlap an area of marker expression.

---
Here we make use of the third-party [MorphoLib](https://github.com/ijpb/MorphoLibJ) library/plugin for morphological operators. To implement this, we simply create a function to use DAPI as a mask for geodesic reconstruction of the marker images:

```python
def apply_mask(marker, mask):
    """Applies a mask to an input binary using geodesic reconstruction.
    :param marker binary image that with be masked
    :type marker ImagePlus
    :param mask binary image that will be used as a mask
    :type mask ImagePlus
    :return reconstructed image
    """
    ip = GeodesicReconstruction.reconstructByDilation(marker.getProcessor(),
                                                      mask.getProcessor(), 8)
    output_imp = ImagePlus("Reconstructed", ip)
    output_imp.copyAttributes(marker)
    return output_imp
```

---
Then we can simply use this function to reconstruct which DAPI cells express the marker.

```python
# Filter segmented marker images with the DAPI channels that we trust
ki67 = apply_mask(ki67, dapi)
ph3 = apply_mask(ph3, dapi)
```