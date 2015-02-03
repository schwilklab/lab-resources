Data Management
===============

author: Dylan Schwilk

## Overview of requirements ##

Metadata is simply data about data. Our data files (such as a table stored as a csv file) do not contain enough information alone in order to reproduce the work or understand the results

## Documenting data (= metadata) Occurs at at least two levels ##

#### At the project level ####

We need to record five pieces of information:

- the context of data collection: project history, aim, objectives and hypotheses
- data collection methods: sampling, data collection process, instruments used, hardware and software used, scale and resolution, temporal and geographic coverage and secondary data sources used
- dataset structure of data files, study cases, relationships between files
- data validation, checking, proofing, cleaning and quality assurance procedures carried out
- information on access and use conditions or data confidentiality, copyright

In the Schwilk Lab, we store this data in a README file at the root directory of the project or subproject. We are in the process of standardizing this format but for now, the file should be in markdown format and each file should have the same sections:

1. Data Context
2. Methods
3. Data Structure
4. Quality Assurance
5. Scripts used
6. Use Conditions

We are still standardizing this, however. Take a look at an example in the [sky island traits repository][traits-distro].

#### At the level of the data files ####

This is already well standardized. We store data in CSV (comma separated values) files. These data files have column headings with short names that are valid R object names. Therefore, we need to store notes and explanations of each column separately. Each data file has a corresponding metadata file which has the same basename with a "-metadata.csv" ending. For example, if the data file is "sensor-soil.csv", then the metadata file in the same directory is "sensor-soil-metadata.csv"

The metadata file has the following columns:

| variable | type | units | description |

and a row for every column in the corresponding data file. For example:

if we have a file "trees.csv":


| tag | date      | spcode | DBH  |
|-----|-----------|--------|------|
| 234 | 5/12/2014 |  QUGR3 | 56.3 |
| 235 | 5/12/2014 |  GUGA  | 20.2 |

Then we should have a file "trees-metadata.csv":

| variable | type    | units | description                                 |
|----------|---------|-------|---------------------------------------------|
| tag      | string  |       | Tree tag number.  All trees tagged at 1.37m |
| date     | date    |       | Date of data collection                     |
| spcode   | string  |       | USDA plant code (See plants.usda.gov        |
| DBH      | numeric | cm    | Tree diameter at breast height              |


## File formats and organization ##

### File formats ###

Plain text (csv) is simplest and portable, but not the most powerful Data base formats (there are open standards). We will try to use csv exclusively

### Directory structures ###

- Use simple informative names
- Use the directory structure itself for organization (very portable).
- Avoid spaces and some special characters in file names. Careful about
  capitalization (lost on some old windows systems).

# Quality assurance #

:TODO:

# Version control and backups

We use [git][git] for version control in the lab. See the [git reference][gitref] for information. We use a central repository workflow and our central repositories are all on [GitHub][github]

The main linux servers in the lab are backed up daily


# Scripts

When using R: have a small number of R scripts that are well commented (with a good description at the top of the file).

Probably best to have separate files for the main analyses and the figures. Or perhaps a cleaned up file that has only the code necessary to create the tables, stats and figures in the submitted manuscript.

See examples in [our git repositories][schwilklab]

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
[schwilklab]: https://github.com/schwilklab
[traits-distro]: https://github.com/schwilklab/skyisland-traits-distro/tree/master/traits/conductance/data/DM-oak-resprouts-2013
