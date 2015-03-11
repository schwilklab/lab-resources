Data Management
===============

author: Dylan Schwilk

## Overview of requirements ##

Metadata means simply data about data. Our data files (such as a table stored as a csv file) do not contain enough information alone for a user to reproduce the work or understand the results. We therefore require additional information stored alongside our data.

## Documenting data (= metadata) Occurs at at least two levels ##

#### At the project level ####

We need to record five pieces of information:

- the context of data collection: project history, aim, objectives and hypotheses. This can be very brief, this is not the manuscript.
- data collection methods: sampling, data collection process, instruments used, hardware and software used, scale and resolution, temporal and geographic coverage and secondary data sources used
- dataset structure. In the Schwilk lab we generally use a separate file for each table rather than a relational database. Therefore we need to understand how files are related to one another (linked tables)
- the data validation, checking, proofing, cleaning and quality assurance procedures that were carried out
- information on access and use conditions or data confidentiality, copyright

In the Schwilk Lab, we store this high level information resides in a README file at the root directory of the project or subproject. We are in the process of standardizing this format but for now, the file should be in markdown format and each file should have the same sections:

1. Data Context
2. Methods
3. Data Structure
4. Quality Assurance
5. Scripts used
6. Use Conditions

We are still working on standardizing this, however. Take a look at an example in the [sky island traits repository][traits-distro].

#### At the level of the data files ####

These metadata describe the variables and units recorded in each data file. This is already well standardized in lab practice. We store data in CSV (comma separated values) files. These data files have column headings with short names that are valid R object names. Therefore, we need to store notes and explanations of each column separately. Each data file has a corresponding metadata file which has the same basename with a "-metadata.csv" ending. For example, if the data file is "sensor-soil.csv", then the metadata file in the same directory is "sensor-soil-metadata.csv"

The metadata file has the following columns:

| variable | type | units | description |

and a row for every column in the corresponding data file. For example:

if we have a file "trees.csv":


| tag | date      | spcode | DBH  |
|-----|-----------|--------|------|
| 234 | 5/12/2014 |  QUGR3 | 56.3 |
| 235 | 5/12/2014 |  GUGA  | 20.2 |

Then we should have a file "trees-metadata.csv":

| variable | type    | units | description                                |
|----------+---------+-------+--------------------------------------------|
| tag      | string  |       | Tree tag number. All trees tagged at 1.37m |
| date     | date    |       | Date of data collection                    |
| spcode   | string  |       | USDA plant code (See plants.usda.gov)      |
| DBH      | numeric | cm    | Tree diameter at breast height (1.37m)     |


## File formats and organization ##

### File formats ###

Plain text (csv) is simple and portable, but not the most powerful format. However, it is what we most commonly use.  It is easy to enter data using a spreadsheet program (eg LibreOffice Calc or Microsoft Excel). Then save the data as ".csv" and choose an csv format options carefully. Do not store any formulas or calculations (the csv file just stores plain text representing either numbers (eg "3.456") or character strings/factor levels (eg "HighNitrogen").  Each column should include only one type of information.

#### Some things to watch out for with csv files ####

- Name your columns with valid R names. Avoid spaces!  In other words, "mass (g)" is a bad column header, but "mass.g" is fine.
- Be careful of any automatic conversion of strings to underlying date/time representation that your spreadsheet program may do without asking you. This could result in loss of information and changing formats upon resaving as plain text.
- Watch character encoding (always use utf-8)
- If you use Microsoft Excel on Mac, be careful of a microsoft bug in which excel will always save csv files using windows style line endings
- If you use commas for field delimiters, then be careful about using commas in any actual data. At the least, you will need to enclose such fields in quotes. Better yet, avoid commas in the data or use tabs for field delimiters.

### Directory structures ###

- Use simple informative names
- Use the directory structure itself for organization --- this improves portability.
- Avoid spaces and some special characters in file names. Be careful about
  capitalization.

# Quality assurance #

Direct digital data entry is the best for quality assurance, because checks can be built in.  For example, if one is entering tree DBH directly on a tablet computer in the field, it is possible to have the data entry system prohibit negative numbers, numbers over some maximum diameter, etc. That said, we most commonly take data in field notebooks and enter them onto the computer that night or a few days later. It is very important that data entry happens soon after data collection, because real quality assurance can't occur until the data are in digital form.

In the Schwilk lab, quality assurance takes the form of R scripts that conduct sanity checks:  sample size matches the study plan, no unexpected, missing data, no impossible numbers (eg negative leaf length), no extreme (impossible) outliers.


# Scripts #

The main tools we use for data analysis are [R][R] and [Python][Python]. I try to help my students toll learn R.

## Some suggestions for code organization ##

Have a small number of R scripts that are well commented (with a good description at the top of the file).

It is probably best to have at least separate files for 1) data reading, cleaning, reshaping; 2) the main analyses and the exploratory figures; 3) a script to create the well formatted tables and figures for the manuscript(s).

See examples in [our git repositories][schwilklab]

# Version control and backups

## Version control ##
Versioning data and code is very important.

We use [git][git] for version control in the lab. See the [git reference][gitref] for information. We use a central repository workflow and our central repositories are all on [GitHub][github]

The Schwilk lab suggested project layout:

```
Main directory (git root)
  README.md
  data
    data_file1.csv
    data_file1-metadata.csv
  scripts
    data-read-clean.R
    stats.R
    figures.R
  figs (dir contents not in version control)
   .gitignore (that excludes all but this file)
  ms
   main-ms.md (or main-ms.tex, or even main-ms.docx)
```

## Backups ##
The main linux servers in the lab are backed up daily using rsnapshot.


# Data management plans required for research proposals #

Many agencies now require data management plans. These usually include:

- which data will be generated during research
- metadata, standards and quality assurance measures
- plans for sharing data
- ethical and legal issues or restrictions on data sharing
- copyright and intellectual property rights of data
- data storage and back-up measures
- data management roles and responsibilities
- costing or resources needed


[git]: http://git-scm.com/
[gitref]: http://gitref.org/
[github]: http://github.com/
[Python]: https://www.python.org/
[R]: http://cran.r-project.org/
[schwilklab]: https://github.com/schwilklab
[traits-distro]: https://github.com/schwilklab/skyisland-traits-distro/tree/master/traits/conductance/data/DM-oak-resprouts-2013
