# Cell scoring revisited
Given a multichannel fluorescent image, we can:

* Identify and count total cells 
* Score the number/proportion of cell that are positive for 2 different markers

---

> "That looks great! Now repeat it with 4 genotypes, 5 treatments, 3 concentrations, 3 fields of view and 5 replicates. Oh, and it could have a developmental effect, so maybe image it over 4 time points."

-- Assoc. Prof.   Idon'tcareif   Youdon'tsleep

---

Thankfully, computers are really good at automating repetitive tasks.

---
# Rapid re-intro to Python programming
Don't worry about the details, the aims are:

* Taste for the logic involved in automating an image analysis workflow.
* Plan early for automation.



```python
# This is a comment
"""So is this"""

# Basic Types and Variables
variable = "This is a string of characters or simply a string"
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