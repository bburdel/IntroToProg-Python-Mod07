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

![Figure 1] (docs/Figure%1.png)

## Error (Exception) Handling
When coding you can actively catch syntax errors or logic errors and debug them. However, there may be errors triggered by the user for which the script can account and avoid. When Python encounters an error during the execution5 of the code it will display an error (exception) message and stop running the script<sup>6</sup>. Code snippet 1, will trigger an exception by attempting to divide by zero (see Exception 1).

```
# --------------------------------------------------------- #
# Title: Exception Handling
# Description: Simple examples of error handling,
#   uncomment code blocks to try them out
# Change Log: (Who, When, What)
# BBurdelsky, 11.28.2021, Created script
# --------------------------------------------------------- #

# Testing code for errors

# No error handling
undefined = 1/0
print(undefined)
```
###### Code Snippet 1

```
Traceback (most recent call last):
  File "/Users/corpuscorvus/Documents/_PythonClass/Week7/Assignment07/Assignment07_ErrorHandling.py", line 12, in <module>
    undefined = 1/0
ZeroDivisionError: division by zero

Process finished with exit code 1
```
###### Exception 1 ZeroDivisionError

### Ways To Handle Errors
#### Try-Except Block
You can use a try-except block of code to help you trap errors7. The try statement will attempt code in that section, testing it for errors. The except portion handles the error. Let's look at this in Code Snippet 2. You can see in Exception 2 that we presented a user-friendly explanation of the ZeroDivisionError.
```
# Try/except block to trap error
try:
   print("Let's try the following equation: \n1/0")
   undefined = 1/0  # this causes an exception
   print(undefined) # we never reach this code
except:
    print("An error occurred. You cannot divide by 0.")
```
###### Code Snippet 2
```
Let's try the following equation: 
1/0
An error occurred. You cannot divide by 0.
```
###### Exception 2. The result of running Code Snippet 2. This shows a custom error message to the user. 

#### Exception Class and Trapping Multiple Exceptions
Python has a built-in exception class that contains the different exception types/sub-classes (with a hierarchy)<sup>8</sup>. If you know the exception that will be triggered, you can use it in a try-except block and present it to the user (this is by capturing the exception object). For instance, a ValueError (in Code Snippet 3) is raised when an operation or function has the right type but an inappropriate value<sup>8</sup>. This occurs when the user enters a string as input but the input cannot be converted to a float number. The resulting messaging presented to the user can be seen in Exception 3. 
```
# Using the Exception Class and passing the exception to a variable
try:
    fltNum = float(input("Enter a number: "))
except ValueError as e:
    print("Oops. That is not a number.")
    print("Python: ", e)
```
###### Code Snippet 3
```
Enter a number: Hello!
Oops. That is not a number.
Python:  could not convert string to float: 'Hello!'
```
###### Exception 3

It is possible to anticipate the several kinds of exceptions a user might raise. You can account for these by listing the exceptions individually in a single except clause (Code Snippet 4) or through multiple except clauses1 (Code Snippet 5). 
```
# Trapping multiple exception types in one except statement
for value in (None, "string"):
    try:
        print("Let's convert", value, "to a float.")
        conversion = float(value)
        print(conversion)
    except (TypeError, ValueError):
        print("This isn't working!")
```
###### Code Snippet 4
```
Let's convert None to a float.
This isn't working!
Let's convert string to a float.
This isn't working!
```
###### Exception 4
```
# Trapping exceptions through multiple except statements
for value in (None, "string"):
    try:
        print("Let's try to convert", value, "to a float.")
        conversion = float(value)
        print(conversion)
    except TypeError as e:
        print("We encountered an issue: ")
        print(type(e), e, e.__doc__, sep="\n")
        print()
    except ValueError as e:
        print("This isn't working!")
        print(type(e), e, e.__doc__, sep="\n")
````
###### Code Snippet 5

Each error type is dealt with in its own exception statement and we can also use the print function to show us the exception’s class (type), the exception’s argument (what is passed to variable e), and  the documentation for that object (.__doc__). The code in Code Snippet 5 results in the output in Exception 5. 
```
Let's try to convert None to a float.
We encountered an issue: 
<class 'TypeError'>
float() argument must be a string or a real number, not 'NoneType'
Inappropriate argument type.

Let's try to convert string to a float.
This isn't working!
<class 'ValueError'>
could not convert string to float: 'string'
Inappropriate argument value (of correct type).

Process finished with exit code 0
```
###### Exception 5

## Summary
We looked at pickling (serialization) data and error handling. As a coding newbie, I cannot think of specific ways in which serialization will be helpful to me outside of it potentially reducing file size and obscuring the file data. Error handling, however, I feel I can immediately put to use. In previous coding assignments I tried to circumvent user error through if-elif statements in loops. For instance, if I was looking for the user to enter a number and they entered a string I would keep prompting the user for a number until they finally entered an acceptable value. Now not only can I circumvent user behavior that way but I can also trap exceptions they might cause by passing ‘bad’ data to the program. 

## Resources
I have used superscripts throughout the text body above, denoting the resource references below to improve readability. (Apologies if this resulted in a hunt.)  

**1** Dawson, Michael. Python Programming, Third Edition. Course Technology, 2010. pgs. 189-216

**2** [pickle — Python object serialization](https://docs.python.org/3/library/pickle.html) 

**3** [What is serialization](https://stackoverflow.com/questions/633402/what-is-serialization)

**4** [5. The import system](https://docs.python.org/3/reference/import.html)

**5** [8. Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)

**6** [Python Exceptions: An Introduction](https://realpython.com/python-exceptions/)

**7** [Python Try Except](https://www.w3schools.com/python/python_try_except.asp)

**8** [Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)

**9** [Binary File](https://en.wikipedia.org/wiki/Binary_file)

**10** [What is the file extension when creating binary files](https://stackoverflow.com/questions/40098510/what-is-the-file-extension-when-creating-binary-files)
