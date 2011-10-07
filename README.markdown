#Introduction
tsub is a very simple batch system written in python. The purpose of this script is to make it easy to utilize all the cpu cores for embarrassingly parallel problem. It basically take a list of command it needs to run and make a process for each one of them while making sure that the number of jobs that is running does not exceed a specified number (defaulted to number of cores). It can be run as a standalone program or as a python module. As a standalone program, you will need to supply a file with a list of commands

#Requirement:
tested on python 2.7 (anything beyond python 2.5 should work)

#Install:
If you want to use it as a standalone link/copy tsub.py to /usr/bin or anywhere in your PATH.
If you want to use it as a module, then copy it to either your project or somewhere in your PYTHON_PATH.

#Usage:
There are two ways to use the script.
Use as standalone. The second argument a file that lists commands. 

    tsub.py cmd

cmd file is as simple as

    python job1.py
    python job2.py
    python fail.py
    #this is comment redirection is also supported
    python job2.py > out1.txt
    python job1.py > out2.txt
    #and it doesn't need to be python script
    du -h
    ls

If you want to use it as a python module, the only method you need is run. See tsub.py for more info on parameters.

```python
import tsub
jobs = ['ls','du -h','date']
#it returns a list of exit codes
exit_codes = tsub.run(jobs)
print exit_codes
```
#Advance Usage:
Sometimes, you may want to run two set of jobs. That is you want 4 data processing jobs in job set A to finish before starting running plotting jobs on set B. This can be accomplish quite easily by just running tsub.run twice.

```python
import tsub
jobs = ['./process 1','./process 2','./process 3']
tsub.run(jobs)
jobs2 = ['./plot 1','./plot 2','./plot 3']
tsub.run(jobs2)
```
