# Files and Exceptions
**Dev:** *BBurdelsky*  
**Date:** *11.20.21*

## Introduction
Previous modules worked with data stored in text files. This week we are working with binary files (files that use bytes instead of standard text)<sup>9</sup>.   Additionally, exception — or error — handling is covered.

## Pickling
Pickle<sup>2</sup> is a built-in module that implements binary protocols to serialize3 and de-serialize an object in Python. It must be imported<sup>4</sup> into the script by using the ‘import’ statement. Pickling allows you to work with and store more complex (than the data you would find in a text file) information (like a list or dictionary) in a binary file. By pickling your data, you obscure the file’s contents and potentially reduce the file size. It is important to note that the file is obscure, not secure<sup>2</sup>. Pickled objects are stored in a binary file (.dat or .bin, or whatever you like as a file extension)<sup>10</sup>. When the open function is used, the mode is specified like this: open(file_name, mode). This handy table<sup>1</sup> contains a summary of binary file access modes.
  
  
| Mode | Description                                                                                                                        |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------- |
| rb	 | Read from a binary file. If the file does not exist, Python will produce an error.                                                 |
| wb	 | Write to a binary file. If the file exists, its contents are overwritten. If the file does not exists, it is created.              |
| ab	 | Append the binary file. If the file exists, new data is appended to it. If the file does not exist, it is created.                 |
| rb+	 | Read from and write to a binary file. If the file exists, its contents are overwritten. If the file does not exist, it is created. |
| wb+	 | Write to and read from a binary file. If the file exists, its contents are overwritten. If the file does not exist, it is created. |
| ab+	 | Append and read from a binary file. If the file exists, new data is appended to it. If the file does not exist, it is created.     |
###### Table 1. Select access modes for binary files. 

Now we will walk through some basic pickling code. You can see the code in Terminal and the resulting file in Figures 1 and 2. 

```
# --------------------------------------------------------- #
# Title: Pickling Demonstration
# Description: A simple example of pickling (a built in
#   function) in Python.
# Change Log: (Who, When, What)
# BBurdelsky, 11.28.2021, Created script
# --------------------------------------------------------- #

# Module statement(s)
import pickle  # imports code from the pickle module

# -----------Data------------------------------------------- #
strFileName = 'GroceryBudgeting.dat'
groceryList = []  # list that will contain to do items
fltCost = None  # will capture user entered cost of item
strItem = ""  # will capture user entered grocery item


# -----------Processing------------------------------------- #
# custom functions to write to and read from a pickled file
def save_data_to_file(file_name, list_of_data):
    objFile = open(file_name, "ab+")
    pickle.dump(list_of_data, objFile)
    objFile.close()


def read_data_from_file(file_name):
    file = open(file_name, "rb+")
    list_of_data = pickle.load(file)
    file.close()
    return list_of_data


# -----------Presentation----------------------------------- #
# Get Item and Cost from user, then store it in a list object
strItem = str(input("Enter a grocery item: "))
fltCost = float(input("Enter the grocery item's cost: "))
groceryList = [strItem, fltCost]

# Store the list object into a binary file
save_data_to_file(strFileName, groceryList)

# Read the data from the file into a new list object and display the contents
print(read_data_from_file(strFileName))
```
###### Listing 1

In listing 1,  pickle.dump( ) writes the pickled object to file and pickle.load( ) reads the pickled object from file2. Figures 1 and 2, show this script running in the command prompt and the resulting pickled file in PyCharm, respectively.



## Error (Exception) Handling

### Ways To Handle Errors
#### Try-Except Block
#### Exception Class and Trapping Multiple Exceptions

## Summary
