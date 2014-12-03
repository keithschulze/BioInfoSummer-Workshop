# Working with Files

Good files naming system:

* Uniquely identifies each file.
* Contains relevant experimental parameters.
* Simple delimiter to separate parameters (e.g., _).
* Don't rely on a set order of files.
* Record dimension data and cropping etc.

Think about this early!

---
Example file naming scheme:
> wt_nacl_5um_1.tif

```python
import os

file_path = "/path/to/folder/wt_nacl_5um_1.tif"
file_name = os.path.basename(file_path)			# wt_nacl_5um_1.tif
file_name = os.path.splitext(file_name)[0]		# wt_nacl_5um_1

# Dimensions data

gen, treat, conc, rep = file_name.split("_")
print gen							# "wt"
print treat							# "nacl"
print conc							# "5um"
print rep							# "1"
```