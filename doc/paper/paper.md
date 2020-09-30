---
title: '`ezc3d`: An easy C3D file I/O cross-platform solution for C++, Python and MATLAB'
tags:
  - C3D
  - C++
  - Python
  - Matlab
authors:
  - name: Benjamin Michaud
    orcid: 0000-0002-5031-1048
    affiliation: 1
  - name: Mickaël Begon
    orcid: 0000-0002-4107-9160
    affiliation: 1
affiliations:
 - name: École de Kinésiologie et de Sciences de l'Activité Physique, Université de Montréal
   index: 1
date: October 1st, 2020
bibliography: paper.bib
---

# Summary
The *c3d* binary format [@crampC3dOrg2019] is an open-source standard extensively used in the field of biomechanics.
Most of the software for data collection and data analysis can read and export *c3d* files. 
Initially, this format was designed to store three-dimensional point data and analog data (e.g., force platform or EMG).
Nowadays, by stretching the standard, companies have managed to include all sorts of theoretically non-standard biomechanical data, including for instance IMU data.
To match the needs of the community, Motion Lab Systems---which created and maintains the *c3d* format---regularly updates the standard to match the biomechanical needs and to include novel usage of the format.

Despite being extensively used by the biomechanics community, there are surprisingly few alternatives when it comes to manipulate *c3d* files outside analyses software. 
This has forced scientists to develop *ad hoc* solutions for each project.
Usually, it requires to write file I/O codes for each software in-house format files. 
While it would make sense to develop a portable solution once for all, as offered by the standardized *c3d* format, the binary nature of the *c3d* format discourages biomechanists from digging into the trouble of developing such a solution.
To our knowledge, `BTK` [@barreBiomechanicalToolKitBTKCore2020] is the most mature (if not, the only) biomechanics library that provides an API to read and write these files.
Unfortunately, despite its open-sourced nature, the project has been mostly abandoned since~2016.
It is more and more out-of-date as it does not follow the changes in the standard of the format.
Unfortunately, due to the intricate connections of its modules, it proved difficult due to update `BTK`.

Introducing the open-source `ezc3d` library which provides a light and comprehensive API to easily read and write *c3d* files. 
For the lay users, `ezc3d` is an up-to-date solution to manage *c3d* files that complies with the latest recommendation of the standard.
It also supports in-house implementations of the main biomechanics software, namely: Vicon, Qualisys, Optotrak, BTS and XSens. 
Fast file I/O is achieved thanks to the C++ core.
MATLAB and Python3 interfaces are also conveniently provided so one can smoothly implement `ezc3d` in their current workflow.
In addition, since the *c3d* standard allows for multiple ways to store force platform data, a force platform analysis module is provided.
The main feature of this module is to express forces and moments in more common reference frames---that is, expressed in the global reference frame calculated at either the origin or at the centre of pressure---so they can be directly interpreted by the user. 

# The dependencies
The `ezc3d` library was originally designed to be a dependencies-free library such that a lay user could easily link `ezc3d` with their project.
Thus, by default, no dependencies are needed to compile nor to use the API.
Moreover, thanks to the absence of external library requirements that could change at any time, `ezc3d` will remain available on all major OS, namely Windows, Linux and Mac. 

By nature biomechanics data are matrix-based data. 
An in-house linear algebra solution was therefore developed to store and manipulate such data.
Our solution will, however, never be as effective as those from dedicated linear algebra libraries.
Hence, thanks to the highly effective `Eigen` linear algebra library [@eigenweb], a fast accessor module is available.

# Current usage of `ezc3d`
The library got the attention of two major software in biomechanics, namely Anybody [@rasmussenChapterAnyBodyModeling2019] and Opensim [@sethOpenSimSimulatingMusculoskeletal2018].
One of the main programmers of the former prepared and maintains the conda-forge recipe for `ezc3d`, so it can be easily installed and updated using conda.
For their version 4.0, Opensim decided to embrace the *c3d* format file by adding the capability to read *c3d* files.
The `ezc3d` library was chosen as the default *c3d* reader back end.

# References