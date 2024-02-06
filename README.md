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


