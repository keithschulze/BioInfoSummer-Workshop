# Looping the analysis procedure
Let's put in the code to run our analysis over a folder full of images.

Break down the requirements:

1. Ask user for a folder of images to analyse.
2. Query that folder to get a list of files to analyse.
3. Filter the list of files to exclude those that are supported.
4. For each file in our list:
    1. Open the image
    2. Analyse the image using the routine we setup previously.
    3. Add results as a new line in the result table.
