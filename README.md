Schwilk Lab Resources
=====================

Repository for lab resources for lab and field work, data management and analyses, and field methods and lab protocols.  [The Schwilk Lab at Texas Tech](https://www.schwilk.org)

Schwilk lab code
----------------

Code for various projects is stored in separate individual git repositories. A few that
might be of most interest for re-use are

- [chiller](https://github.com/schwilklab/chiller): Code to run a temperature profile program on the Thermo-Fisher refrigerated bath.
- [serial-balance](https://github.com/schwilklab/serial-balance): Communicate with an analytical balance.
- [pandoc-build-system](https://github.com/schwilklab/pandoc-build-system)
- [skyisland-climate](https://github.com/schwilklab/skyisland-climate): Example of a fairly well documented and organized repository for a large project.
- [emacs-starter](https://github.com/schwilklab/emacs-starter): Fairly lightweight emacs starter package (.emacs.d config files) for my students so you setup will be not too different from mine.

File organization in this repo
------------------------------

### data-code ###

Information on lab data management, code and version control

- [Git and GitHub](data-code/git-and-github.md): Our lab guide to using git and GitHub for collaboration.
- [data-management](data-code/data-management.md): Our current lab best practices for managing lab data, setting up a project, organizing code and keeping the whole thing in version control


### equipment ###

Equipment lists and maintenance histories

[TODO] - add history of balance repairs and calibration

[TODO] - Organize equipment list that has been started; organize into categories such as field equipment, plant phys, etc; correct names and give manufacturer; correct location information in more detail.

### html ###

Holds script to build html version of these local markdown files.

[TODO] - remove or rename this?  Is this necessary?


### lab-org ###

This folder folder for information on lab business, scholarships and funding, data management, etc.

- [computers-network](lab-org/computers-network.md): Instructions and description of our lab computer network
- [field-work-checklist](lab-org/field-work-checklist.md): Use this checklist when packing for the field!
- [funding-opportunities](lab-org/funding_opportunities.md): List of graduate fellowships and scholarships
- [lab-business](lab-org/lab-business.md): For information on mailing packages, departmental contacts, orderings supplies


### methods ###

Experimental methods and protocols. See individual files. Includes folder for plant identification tools:


#### plant-id ####

We'd like to add a key to plants of Lubbock County and that will be an ongoing project aided by collections students make in BIOL-3306.

- [Schwilk Lab Guide to Major Angiosperm Families](plant-id/common-angiosperm-families.md)
- [External plant identification resources](plant-id/external-resources.md)

### safety ###

Lab safety plan and safety protocols

- [schwilk-lab-safety-plan](safety/schwilk-lab-safety-plan.md): Our EHS required safety plan. Individual safety protocols covered separately
- [chainsaw-safety-protocol](safety/chainsaw-safety-protocol.md): Chainsaw safety.
- [bleach-safety-protocol](safety/bleach-safety-protocol.md): Bleach safety.

Instructions for editing
------------------------

These files are all stored in markdown format (https://daringfireball.net/projects/markdown/ , see also https://help.github.com/articles/github-flavored-markdown)

If these are methods on which you are working, feel free to edit and commit changes or create an issue first to give folks a heads up on the proposed changes.

Although it is ok to commit to master, a good workflow on a shared repository is:

  1. Make a working branch for yourself.  You can even push this branch to the repository, in that case, make sure to give it a descriptive name involving the planned work or perhaps your name.
  2. Do you work in this branch and commit often.
  3. Issue a pull request so others can review your work before it is merged into /master.

  This may be overkill for the protocols repository, but may make sense for others.

Important Note:
---------------

The plan is to make this repository public. Because it is very difficult to actually delete anything from a git repository, it is important to never commit any private information we don't want shared. I don't think there is much chance of that, but I just wanted to warn everyone.
