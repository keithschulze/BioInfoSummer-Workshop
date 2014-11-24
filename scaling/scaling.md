# Looping the analysis procedure
Let's put in the code to run our analysis over a folder full of images.

Break down the requirements:

1. Ask user for a folder of images to analyse.
2. Query that folder to get a list of files to analyse.
3. Filter the list of files to exclude those that are not supported.
4. For each file in our list:
    1. Open the image
    2. Analyse the image using the routine we setup previously.
    3. Add results as a new line in the result table.

Note: We might also like to include some code to save the segmented binary images, so that users can check the outputs of our script. For that we need to ask the user for an output folder and get image to save the segmented binary images into that folder.

```python
def run():
    # Get the user to choose a directory of images to analyse
    dc = DirectoryChooser("Pick a folder of images to analyse...")
    img_dir = dc.getDirectory()

    if img_dir is None:
        print "No directory selected."
        return

    # Get the users to specify an output directory
    od = DirectoryChooser("Pick an output folder...")
    output_dir = od.getDirectory()

    # Get a list of files from the input directory
    file_list = os.listdir(img_dir)
    file_list = filter(accept, file_list)

    results = ResultsTable()

    # Iterate through the list of files
    for fp in file_list:
        image = IJ.openImage(os.path.join(img_dir, fp))

        # ... code that analyses image from v4 of the script
        # ...
        # ...

    results.show("Results")

run()
```