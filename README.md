# NeelBook
NeelBook is a CLI tool to generate code based on configuration in json format, for all programing languages

# Commands
To view all available commands:
```
neelbook
```

To create a new project
```
neelbook new [name]
```
To view all available plugins (plugins are templates)
```
neelbook plugin list
```
To add remove plugins :
```
neelbook plugin add [name]
neelbook plugin remove [name]
```
To execute code generation using templates:
```
neelbook run
```


# Creating/Updating templates

## Basic Syntax
We have three kinds of contents:
1. Normal text: this is the text will be printed to the outout documents without any processing
2. Line statements: These are lines start with the code   //## 
3. Inline statements: These are code between ((## and ##)) the code between them will be evaluated and printed automatically
for example:
```
Normal text
//## LINE STATEMENT
Normal text ((## INLINE STATEMENT ##)) Normal text 
Normal text
```
### Define Variable
You can define string, integers and json content formats like the following:

```
//## str myStringVar = "Hello world"
//## int myInteger = 5
//## json myJsonConfig = "./metadata.json"
```
When you declare json, the system will load its content to this variable
### Assign Value to Variable
This is similar to declaration but no need to the variable type keyword:
```
//## myStringVar = "Hello world"
//## myInteger = 5
//## myJsonConfig = "./metadata.json"
```
#
You can also append value to string and integer variables:
```
//## myStringVar += " my dear"
//## myInteger = 3

```
#
To print out variables in the templates you can use print statement:
```
//## print myInteger
//## print myStringVar
```
#
You can add remarks to any statements using the keyword *rem*, so it will not be executed.
```
//## rem THIS WILL BE IGNORED
```
### Controlling flow
You can use *if* statement as following:
```
//## if myInteger = 5
//## rem BEFORE END YOU CAN PUT IF BODY
//## end

//## if myInteger >= 5
//## rem BEFORE END YOU CAN PUT IF BODY
//## end

//## if myInteger <> 5
//## rem BEFORE END YOU CAN PUT IF BODY
//## end

//## if myStringVar = "Text goes here"
//## rem BEFORE END YOU CAN PUT IF BODY
//## end
```
#
You can use *for* statement as following:

```
//## for counter = 5
//## rem This will be executed 5 times
//## end
```
The starting value is one and the last value was speficied in the for declaration

#

You can access array in the json file and create loops using them like the following:

```
//## json myJsonFileContent = './myJsonFile.json'
//## foreach item = myJsonFileContent.array
//## rem Foreach body
//## end
```
Please not you can access sub array of other json elements like this:
```
//## json myJson = './myJsonFile.json'
//## foreach item = myJson.section1.subSection1.array
//## rem Foreach body
//## end
```
#

### String Functions

let's define a string variable called x1 equals to "AppLibTest" and use string functions aginst it:

Command | Result 
--- | --- 
```x1``` | AppLibTest 
```camel(x1)``` | appLibTest 
```pascal(x1)``` | AppLibTest 
```snake(x1)``` | applibtest 
```kebab(x1)``` | applibtest 
```spacer(x1)``` | App Lib Test 
```hyphen(x1)``` | app-lib-test 
```lower(x1)``` | applibtest 
```upper(x1)``` | APPLIBTEST 
```replace(hyphen(x1) "-" "/")``` | app/lib/test 

let's define another string variable called y1 equals to "Book Library" and use string functions aginst it:

Command | Result 
--- | --- 
```y1``` | Book Library 
```camel(y1)``` | bookLibrary 
```pascal(y1)``` | BookLibrary 
```snake(y1)``` | book_library 
```kebab(y1)``` | book-library 
```spacer(y1)``` | Book  Library
```hyphen(y1)``` | book -library
```lower(y1)``` | book library 
```upper(y1)``` | BOOK LIBRARY
```replace(hyphen(y1) "-" "/")``` | book /library



## Control Output files
All output statements start with *output* keyword
by default all output files will by located in output folder, the output filename by default will be the same source template file but without the extension ".t"
This behavior can be customized using the output statements
### Output Location
You can change the file name and file location using the following statement:
```
//## output location "./outout.cs" 

//## output location anyStringVariable 
```
That statement will override the distination file with the new file
### Cancel the output override mode
To stop overriding files you can use this:
```
//##  output mode "DoNotOverride"
```

### Output After
By default the output files will put output content in new file, but you can put the content inside the output file after speficit line using the following statement:
```
//## output after "//_some keyword in output file" 

//## output after anyStringVariable 
```
Please note that the output content will be checked not to be duplicated in the distination file
### Output replace section
You can replace the whole section of content file if you provide both *after* and *before* keywords:
```
//## output after "//_begin block" 
//## output before "//_end block"
```
