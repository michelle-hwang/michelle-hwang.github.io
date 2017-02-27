---
tags:
  - resource
---

A big aspect of programming is the user interface. This goes for people who are going to be using what you code, and also for others who want to work on your code. It's extremely frustrating when you try to execute a script someone wrote and you can't figure out why it's not working! 

Python has a convenient module called ```argparse``` that lets you create easy-to-use user interfaces for your scripts. I now use it for every script I write so I can simply type ```script.py -h``` to figure out what my script does and what parameters it takes, optional or not!

### Basics

It's very easy to use. Simply import the module:

```import argparse```


And then generate a parser object. This is what you will use to specify command line arguments for your script to be parsed. It's also where you can add a description to your script that will show up when you execute it with ```-h```.

```parser = argparse.ArgumentParser(description='This is a description of your script.')```


Let's add an argument. This is a mandatory argument and must be specified in order for the script to run.

```parser.add_argument('infile', help='Mandatory name of infile for script.')```


To specify an optional argument, preface it with a '-':

```parser.add_argument('-n', help='Number of repetitions.')```


Finally, to parse all the arguments you have specified into an arguments object:

```args = parser.parse_args()```


This object will hold all of your arguments and they can be accessed by calling it by name:

```infile = open(args.infile, 'r')```


### Intermediate



