#Introduction
tsub is a very simple batch system written in python. The purpose of this script is to make it easy to utilize all the cpu cores for embarrassingly parallel problems. It basically take a list of commands you want to run and make a process for each one of them while making sure that the number of jobs that is running does not exceed a specified number (defaulted to number of cores). It can be run as a standalone program or as a python module.

#Requirement:
Tested on python 2.7 (anything beyond python 2.5 should work)

#Install:
If you want to use it as a standalone link/copy tsub to /usr/bin or anywhere in your PATH.
If you want to use it as a module, then copy it to either your project or somewhere in your PYTHON_PATH.

#Usage:
There are two ways to use the script. Standalone or as a module in python code.

##Standalone
Use as standalone. The second argument a file that contains list of commands. 

    tsub cmd

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

##Module
If you want to use it as a python module, the only method you need is tsub.run. Here is an example. The second argument is optional maximum number of running jobs. It defaults to number of cores.

```python
import tsub
jobs = ['ls','du -h','date']
#it returns a list of exit codes
exit_codes = tsub.run(jobs)
print exit_codes
```

#Tips:
Sometimes, you may want to run two set of jobs. That is you may want 4 data processing jobs to finish before start running plotting jobs. This can be accomplished quite easily by just running tsub.run twice. This may seem obvious but is quite useful.

```python
import tsub
jobs = ['./process 1','./process 2','./process 3']
tsub.run(jobs)
jobs2 = ['./plot 1','./plot 2','./plot 3']
tsub.run(jobs2)
```
