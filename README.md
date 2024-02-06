<h1>Generate a Disk Usage Report with Python</h1>

<h2>Description and Objectives</h2>

In this project I created Python script to generate a disk usage report on an Ubuntu Linux system. The script was used to measure total disk usage for each file and directory in the system, and generate a CSV file for the report.</b>

<h2>Project walk-through</h2>

<h3><p align="center">1.Prepare the directory: </h3>

Firstly, I created a new directory to house the script from the terminal:</b>

```mkdir python_scripts```
</b>

Next, I generated the script file itself:</b>

```touch  python_scripts/disk_report.py```</b>

This way, I was able to open the new directory within Visual Studio Code from the command line:</b>

```code python_scripts```</b>

<p align="center"><img width="70%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/ef25dbc4-c7ab-4093-ab77-de38ce38c5d9">


Within the newly created disk_report.py, I added a shebang line at the very start of the file to identify what program is interpreting the code:</b>

```#!/usr/bin/python3```</b>

<h3><p align="center">2.Import sys to access the command line: </h3>

In this part of the task, I needed to import the `sys` library to be able to access the command line from my Python script and create the main program. `sys` provides access to some variables used or maintained by the interpreter and functions that interact closely with the interpreter.</b>

I added the `if __name__ == “__main__”` conditional statement, which allows any nested code to be executed when the file runs as a script. By passing the file object to the Python interpreter, the expression `__name__ == "__main__"` returns `True`. This idiom allowed me to check whether the file was running as a stand-alone program.</b>

Next, I assigned the default value to the directory path as `/home` so that, in case the command line argument was not available, a default path would be in place.</b>

After that, I wanted to check the number of command line arguments that were passed. For this reason, I printed the following: </b>

`print('total arguments passed: ', len(sys.argv))`</b>

`sys.argv` is a list in Python that contains all the command line arguments passed to the script.
The output of the print showed that, at that moment, the total arguments passed amounted to one, namely the script itself (`disk_report.py`).
However, when I ran the script with an additional command line argument (`./disk_report.py /home/`) the amount of argument passed was two.</b>

Now, I needed to assign a `directory` variable, depending on whether an additional argument was passed beside the script itself. For this, I used the following code:</b>

`directory = sys.argv[1] if len(sys.argv) >= 2 else path`</b>

This means that the value assigned to the variable `directory` should the second argument passed in case there are two or more arguments. In case the total number of arguments is less than two, the default value should be the value assigned to `path` (in this case `/home`).</b>

<p align="center"><img width="70%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/efbd8cbf-0ac2-40aa-942a-4432578d28f2">




