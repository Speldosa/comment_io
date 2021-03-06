# Name
comment_io


# Version: 
1.2


# Last updated: 
2015-11-19


# Author: 
Martin Asperholm, martin.asperholm@gmail.com


# License type:
GNU General Public License, version 3


# Description:
comment_io is a small script written in Python to help you to automatically remove and uncomment lines in your code. The program was sprung out of a need I myself had of turning on and off certain environments in LaTeX. After digging around, trying to make this happen by using only LaTeX code, I finally got fed up and just wrote this program instead.

Basically, you use the program by marking certain lines in your code with certain commands. The program then detects these commands and removes or uncomment the whole line depending on which mode you’ve set it to.


# Basic usage: 
Place the python file, comment_io.py, in the directory where the file you want to manipulate is located. Then type:

	python comment_io.py 'Name of original file' 'Name of output file' 'Program mode' 'List of commands'

in the terminal. The option parameters are more thoroughly explained below:

* *Name of original file* - The name (or path and name if it’s not placed in the same directory as the program) of the original file that should be manipulated.
* *Name of output file* - The desired name (or path and name) of the output file that the program generates.
* *Program mode* - Possible parameters are either ‘in’ or ‘out’. Tells the program whether it should be in in mode (where lines are uncommented) or out mode (where lines are removed). 
* *List of commands* - A list, separated by spaces, of all the commands that should be detected by the program and used to remove or uncomment lines but without the initial comment character/s.

## Example 1:
	
	python comment_io.py Test.tex NewFile.tex out %@

Here, all the lines in the file Test.tex that contains ‘%@‘ will be removed. The result is printed to NewFile.tex. That is, if the original file looked like this:

	This is a test. %@
	This is another test.

The modified file will look like this:

	This is another test.


## Example 2:

	python comment_io.py Test.tex NewFile.tex in %@

Here, all the lines in the file Test.tex that begins with ‘%@‘ will be uncommented (by removing all instances of ‘%@‘). The result is printed to NewFile.tex. That is, if the original file looked like this:

	%@ This is a test.
	This is another test.

The modified file will look like this:

	This is a test.
	This is another test.

## Example 3:

	python comment_io.py Test.tex NewFile.tex out %@ %optional

Here, all the lines in the file Test.tex that contains either ‘%@‘ or ‘%optional’ will be removed. The result is printed to NewFile.tex. That is, if the original file looked like this:

	This is a test. %optional
	This is another test. %@
	This is yet another test.

The modified file will look like this:

	This is yet another test.

# Practical usage

## Example:

In LaTeX, one might sometimes wish to be able to turn on and off certain environments depending on the desired output. While this sometimes can be done within LaTeX itself, other times it can prove to be really hard to get working. For example, let's say that you had a file, 'Test.tex', that looked like this:

	\documentclass{article}
	\begin{enumerate}
		\item
		This is a test.
		\begin{enumerate}
			\item 
			This is another test.
		\end{enumerate}
		\item
		This is yet another test.
	\end{enumerarate}
	\end{document}

and that you wanted the option to, on the fly, turn of the main enumerate environment but not the nested. This can easily be achived with the help of comment_io. First, just mark all the lines that should be affected, like so:

	\documentclass{article}
	\begin{enumerate} %remove
		\item %remove
		This is a test.
		\begin{enumerate}
			\item This is another test.
		\end{enumerate}
		\item %remove
		This is yet another test.
	\end{enumerarate} %remove
	\end{document}

Then run:

	python comment_io.py Test.tex NewFile.tex out % remove

This would result in a new file, NewFile.tex, that would look like this:

	\documentclass{article}
		This is a test.
		\begin{enumerate}
			\item This is another test.
		\end{enumerate}
		This is yet another test.
	\end{document}

Typesetting this file would only output one enumerated item, namely the 'This is another test' part.


# Change log

v1.2 (released 2015-11-19):
* Simplified the program significantly. Made it so that 'in' now simply removes instances of the command and so that 'out' now simply removes whole lines.

v1.1 (released 2015-06-29): 
* Fixed some bugs.
* Improved the readme file with useful tips of when to use the program.
* Corrected some aspect of the readme file that didn't adhere to the Markdown standard.

v1.0 (released 2015-05-12): 
* Added all the basic functionality.
