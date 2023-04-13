Data Management
===============

author: Dylan Schwilk

# Overview #

All of our work involves data. With multiple simultaneous projects ranging in size from a few rows to millions of records, it is important that we are organized. Data management means

1. Recording data in a way that loses no information (format decisions, metadata)
2. Ensuring that all data are collected and none goes missing (version control, backups)
3. Ensuring that we (and others) can understand our data months or years from now (metadata)
4. Keeping a record of all decisions regarding our data, all transformations, all reshaping, all corrections (scripts, version control)
5. Visualizing and analyzing our data (usually R scripts)

## Directory structures ##

Some recommendations:

- Use simple informative names
- Use the directory structure itself for organization --- this improves portability.
- Avoid spaces and some special characters in file names. Be careful about
  capitalization.

The project layout that Dylan uses most of the time shown below. I've shown a few example file names but most are not shown.

```
Main directory (git root)
  README.md
  data
    data_file1.csv
    data_file1-metadata.csv
  ms
    main-ms.md (or main-ms.tex, main-ms.docx)
  results (directory contents not in version control)
    .gitignore (with two lines, see below)
    figure1.pdf
    figure2.pdf
  scripts
    data-read-clean.R
    stats.R
    figures.R
```

### `root` 

This is the main directory and the root of the git repository if in version control. This folder will be named for the project (eg `sky-island-climate`) and should have a README describing the project and explaining where there data and code are. This folder will also ahve any global `.gitignore` file (see version control, below)

### `data` ###

Store data and file specific metadata here. Use comma-separated-values (csv) files for data. Store data in a tidy format when possible with one row per observationa nd one column per measured or grouping variable. Store data with different types of observations in different files.  For example:

- trees.csv : one row of data per each tree sampled. Columns: `tree_id`, `DBH`, `species_code`
- species.csv : one row of data per species in the data set. Columns: `species_code`, `genus`, `specific_epithet`, `family`.

### `ms` ###

Keep your manuscript or thesis text here. You might use MS Word for your manuscript or you could use a plain text format such as markdown, org mode, LaTeX.

### `results` ###

This directory is only for files that are created automatically by code. Nothing in this directory is in version control. But git will not add empty directories to a repository. Therefore, to ensure that a fresh clone of the git repo will include this directory although it is empty, place a `.gitignore` file in it with the following two lines:


```
*
!.gitignore
```

This tells git to ignore all files in this directory except for the .gitignore file itself. A fresh clone of the repository will include the results directory and the .gitignore file.


### `scripts` ###

Keep your anlayses code here (usually this will be R scripts). I think current best practice is to write scripts so that they assume the working directory is the root of the repository. In that case, any references to data files will have paths something like `./data/species.csv`. This is consistent with how RStudio and Emacs both behave be default: barring any other settings, they assume that the working directory for a new process should be the "project" root and git repos indicate projects. Then all reference to other files use relative paths. For example, output figures are saved to the results folder (eg `./results/fig1.pdf`). This means to call command-line scripts one must do so from the root folder.  Alternatively, as long as it is documented, you can write your R code so that scripts assume the working directory `/scripts` folder. See [R and the working directory](#R-and-the-working-directory), below.


# Storing and documenting data #

## File formats ##

Plain text, such as [comma separated values format (csv)][csv], is simple and portable. It is not the most powerful format, but it is what we most commonly use. It is easy to enter data using a spreadsheet program (eg LibreOffice Calc or Microsoft Excel). Then save the data as ".csv" and choose an csv format options carefully. Do not store any formulas or calculations (the csv file just stores plain text representing either numbers (eg "3.456") or character strings/factor levels (eg "HighNitrogen").  Each column should include only one type of information.

### Some things to watch out for with csv files ###

- Name your columns with valid R names. Avoid spaces! In other words, "mass (g)" is a bad column header, but "mass_g" is fine.
- Be careful of any automatic conversion of strings to underlying date/time representation that your spreadsheet program may do without asking you. This could result in loss of information and changing formats upon resaving as plain text.
- Watch character encoding (always use utf-8)
- If you use Microsoft Excel on Mac, be careful of a microsoft bug in which excel will always save csv files using windows style line endings
- If you use commas for field delimiters, then be careful about using commas in any actual data. At the least, you will need to enclose such fields in quotes. Better yet, avoid commas in the data or use tabs for field delimiters.


## Quality assurance ##

Direct digital data entry is the best for quality assurance, because checks can be built in. For example, if one is entering tree DBH directly on a tablet computer in the field, it is possible to have the data entry system prohibit negative numbers, numbers over some maximum diameter, etc. That said, we most commonly take data in field notebooks and enter them onto the computer that night or a few days later. It is very important that data entry happens soon after data collection, because real quality assurance can't occur until the data are in digital form.

In the Schwilk lab, quality assurance takes the form of R scripts that conduct sanity checks: sample size matches the study plan, no unexpected, missing data, no impossible numbers (eg negative leaf length), no extreme (impossible) outliers.


## Metadata ##

Metadata means simply data about data. Our data files (such as a table stored as a [csv file][csv]) do not contain enough information alone for a user to reproduce the work or understand the results. We therefore require additional information stored alongside our data. Documenting data (= metadata) occurs at at least two levels.

### At the project level ###

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

### At the level of the data files ###

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
|----------|---------|-------|--------------------------------------------|
| tag      | string  |       | Tree tag number. All trees tagged at 1.37m |
| date     | date    |       | Date of data collection                    |
| spcode   | string  |       | USDA plant code (See plants.usda.gov)      |
| DBH      | numeric | cm    | Tree diameter at breast height (1.37m)     |

# Code #

The main tools we use for data analysis are [R][R] and [Python][Python]. We also use shell scripts ([Bash][bash]) to glue various other pieces of code and existing software together. I help my students to learn R and I teach a course in R programming, so this is the most common language we use.

## R and the working directory ##

It is best to avoid any explicit calls to set the working directory in your R code (avoid `setwd()`). Therefore, you must standardize on an assumed working directory. In our projects, the scripts are all placed in a `scripts` directory and the code in these scripts either assumes that this is the working directory or that the repository root is the working directory. Newer projects use the latter convention. In other words, to refer to a data file in the data directory, use relative paths: `"./data/some-data-file.csv"`. The ways of ensuring that your editor/IDE set the startup working directory vary by system (eg `.Rproj` files for RStudio). These system-specific files should NOT be tracked by git and are specific to each user. The `.gitignore` should list those file types.


## Some suggestions for code organization ##

Have a small number of R scripts that are well commented (with a good description at the top of the file).

It is probably best to have at least separate files for 1) data reading, cleaning, reshaping; 2) the main analyses and the exploratory figures; 3) a script to create the well formatted tables and figures for the manuscript(s).

See examples in [our git repositories][schwilklab]


# Version control #

## Version control ##
Versioning data and code is very important.

We use [git][git] for version control in the lab. For an outline of our git and [GitHub][github] workflow see [git and Github instructions](./git-and-github.md).


# Backups #

The main linux machines in the lab are backed up daily using our rsnapshot scripts.

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

[bash]: http://www.gnu.org/software/bash/
[csv]: http://en.wikipedia.org/wiki/Comma-separated_values
[git]: http://git-scm.com/
[gitref]: http://gitref.org/
[github]: http://github.com/
[Python]: https://www.python.org/
[R]: http://cran.r-project.org/
[schwilklab]: https://github.com/schwilklab
[traits-distro]: https://github.com/schwilklab/skyisland-traits-distro/tree/master/traits/conductance/data/DM-oak-resprouts-2013
