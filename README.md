<h1>Generate a Disk Usage Report with Python</h1>

<h2>Description and Objectives</h2>

In this project I created a Python script to generate a disk usage report on an Ubuntu Linux system. The script was used to measure total disk usage for each file and directory in the system, and generate a CSV file for the report.</b>

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

<h3><p align="center">3.For loop to retrieve directories: </h3>

The goal of this task was to create a `for` loop to access each sub-directory within the main path (`/home`).</b>

For this, I imported `os`, which is a Python built-in module that includes methods for interacting with the operating system, like creating files and directories, fetching their content, changing, and identifying the current directory, and more.</b>

I added a `for` loop to retrieve all the directories and iterate through each one of them to print their full path. In this case, I employed the `os.scandir()` method, which extracts the entries in the directory given by the specified path.</b>

Next, I needed to check if the same entries were actually directories. For this, I employed a conditional statement followed by `.is_dir(follow_symlinks=False)` method. The `follow_symlinks=False` parameter is instructing the script to ignore and omit any symbolic links from the printed list. 
</b>


<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/773aeed0-1d08-47ca-ae5c-d0c465e73858">

Results:</b>
<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/9763d5bd-0005-4b85-b60d-ef65e44e3a4b">

<h3><p align="center">4.Determining disk space: </h3>

In this task, I created a function to determine the disk space used by each of the directories previously identified.</b>

I started by defining the function as `get_size` and passing `path` as the argument.
I then assigned the value `0` to the variable `total`, which is going to be returned at the end of the function. The total size for each directory is going to be determined by repeating the same `for` loop employed to identify the directories (see previous step).</b>

There could be instances where an error occur in case a directory is inaccessible, for whatever reason. To avoid script crashes, I used the `try` and except `block`, in conjunction with a conditional statement to check whether the entry encountered by the script, is a directory:</b>

```
If entry.is_dir(follow_symlinks=False):
	total += get_size(entry.path) 
else:
	total += entry.stat(follow_symlinks=False).st_size
```
</b>

The above would give me the total size of the directories. In case the entry is not a directory, `entry.stat` will provide the statistics of the file that we have encountered, as well as the file size (`.st_size`).</b>

Finally, I raised the exception, with `e` working as an alias, requesting to print the exception itself.</b>

<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/075c7df3-c863-454c-ae1e-83365dd03d02">

Once the `return` statement was added to close the function, I printed the function itself, right underneath the end of the original `for` loop:</b>

```print(get_size(entry.path))```
</b>

<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/f6f508e8-027f-4c44-9499-a0c15c566daf">


Results:</b>

<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/9d0b0962-59b7-4047-a09a-21ea8f4760e8">

<h3><p align="center">5.Generate the CSV: </h3>

In the final part of the project, I imported `pandas` library to create the data structure necessary to generate the CSV file containing the disk usage report. `pandas` is most used to work with data sets. It has functions for analysing, cleaning, exploring, and manipulating data.</b>

Into the main program, right underneath the command line argument count, I added two empty lists. `usage` is going to be populated by disk usage information, whilst `paths` is going to include the directory paths. Within the `for` loop below those, I appended the empty lists with, respectively, usage information and entry path information.</b>

Next, within the `usage_dict` variable, I went to set the structure of the dictionary that will be populated with the information coming from `usage` and `paths` lists:</b>

```
usage_dict = {‘directory’ : paths, ‘usage’ : usage}
df = pd.DataFrame(usage_dict)
```
</b>

Within the variable `df`, `pd.DataFrame` helped to translate the keys and values contained in `usage_dict` into a fixed, bidimensional grid that can be easily overviewed within the final CSV file.</b>

After printing the variable `df`, I exported the final report into CSV by using the following solution:</b>

```df.to_csv(“disk_home_usage.csv”)```
</b>

<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/8caafa4e-cb71-4898-992c-888ffe51dd52">

Results:</b>

<p align="center"><img width="60%" alt="image" src="https://github.com/matteoarnetoli/disk_usage_repot_python/assets/152484037/96907589-2361-44d1-a686-c42f0c7050ab">



