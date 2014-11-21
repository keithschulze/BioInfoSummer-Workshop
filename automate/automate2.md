# Cleaning up the code

We can introduce functions to encapsulate certain tasks and break the code up into logical blocks.

---
Create a function to splits channels and return them separate images.

```python
def split_channels(image):
    """Split a 3-channel image and returns the 3 separate channels.
    :param image input image
    :type image ImagePlus
    :return tuple containing 3 individual channels
    """
    channels = ChannelSplitter.split(image)
    return channels[0], channels[1], channels[2]

img = IJ.getImage()
ki67, ph3, dapi = split_channels(img)
#... rest of code
```

---
Next, we can create functions for segmentating different channels. The same segmentation procedure is used for both Ki67 and Ph3, so one function will work for both. DAPI needs an extra watershed steps to split touching cells, so it gets a separate function.

```python
def segment_marker(img):
    """Segment marker channel by Li autothreshold and output binary.
    :param img input image
    :type img ImagePlus
    :return segmented binary image
    """
    img.getProcessor().setAutoThreshold(AutoThresholder.Method.Li, True)
    IJ.run(img, "Convert to Mask", "")
    return img


def segment_dapi(img):
    """Segment DAPI channel by Li autothreshold, perform watershed to split
    cells and output binary.
    :param img input image
    :type img ImagePlus
    :return segmented binary image
    """
    img.getProcessor().setAutoThreshold(AutoThresholder.Method.Li, True)
    IJ.run(img, "Convert to Mask", "")
    IJ.run(img, "Watershed", "")
    return img
```

These are simply applied as such:

```python
# Segment DAPI image and split cells using watershed
dapi = segment_dapi(dapi)

# Segment Ki67 image
ki67 = segment_marker(ki67)

# Segment Ph3 image
ph3 = segment_marker(ph3)
```

