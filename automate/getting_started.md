# Why automate? Cell scoring revisited
Given a multichannel fluorescent image, we can:

* Segment and count total cells 
* Score the number/proportion of cell that are positive for 2 different markers

---

> "That looks great! Now repeat it with 4 genotypes, 5 treatments, 3 concentrations, 3 fields of view and 5 replicates. Oh, and it could have a developmental effect, so maybe image it over 4 time points."

__Assoc. Prof.   Idon'tcareif   Youdon'tsleep__

<br>
That's 10,800 individual images to process.

Thankfully, computers are really good at automating repetitive tasks.

---

Let's remind ourselves of the process for scoring cells manually:

1. Split the DAPI, Ki67 and Ph3 channels, so we can work on them separately.
2. Segment DAPI:
    1. Threshold using Li AutoThreshold.
    2. Watershed to split cells.
3. Segment Ki67:
    1. Threshold using Li AutoThreshold.
4. Segment Ph3:
    1. Threshold using Li AutoThreshold.
5. Count cells in DAPI binary using Particle Analysis
6. Count cells in Ki67 binary using Particle Analysis
7. Count cells in Ph3 binary using Particle Analysis

Note: We will introduce Geodesic reconstruction again later.

---
## Rapid re-intro to Python programming
Don't worry about the details, the aims are:

- Taste for the logic involved in automating an image analysis workflow.
- Plan early for automation.


```python
# This is a comment
"""So is this"""

# Basic Types and Variables
variable = "This is a string of characters (or simply a string)."
another_variable = "Hello, world!"
five = 5
exact = 10.23
liar = True

# We can also define functions. Think of these like
# a mathematical function.
# e.g. y = x²
def square(x):
	return x*x
	
y = square(2)
print y 				# outputs 4

# It doesn't have to be mathematical though
def say_hello(name):
	print "Hello, " + name
	
say_hello("john") 		# outputs: Hello, John
```

We will also make use of many functions/tools that are defined in the ImageJ core libraries and its plugins:

```python
from ij import IJ, ImagePlus, ImageProcessor
from ij.measure import ResultsTable
from ij.plugin import ChannelSplitter
```

Admittedly, these are not very discoverable, but here are a couple useful resources to get you started:

- [Image developer documentation](http://rsb.info.nih.gov/ij/developer/index.html)
- [ImageJ API documentation](http://rsb.info.nih.gov/ij/developer/api/)
- [Fiji Jython scripting introduction](http://fiji.sc/Jython_Scripting)


## A note on ImagePlus and ImageProcessor
[ImagePlus](http://rsb.info.nih.gov/ij/developer/api/ij/ImagePlus.html) and [ImageProcessor](http://rsb.info.nih.gov/ij/developer/api/ij/process/ImageProcessor.html) are very important data abstractions i.e., this is how images are represented in ImageJ. 

ImagePlus:

- Underlying programmatical structure used to represent a multi-dimensional image in ImageJ.
- Hold important information like the size of each dimension, bit-depth of pixels, calibrations, metadata and much more.
- Pixel data for each plane of the image is store in an ImageProcessor.

ImageProcessor:

- Has functions for accessing and manipulating actual pixel data for a particular image plane.

Don't worry if this is not immediately clear, just understand that underlying the images you see in the ImageJ user interface is an ImagePlus and that each image plane has an ImageProcessor.