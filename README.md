# TESS Stellar Variability Catalog Analysis @ ARDASTELLA
![Ardastella_logo](https://github.com/user-attachments/assets/9b2b480b-0743-43da-a0c6-7212f9db9e1a)
## Background and Overview
ARDASTELLA is a research group consisting of University faculty, PhD students, and international collaborators working on pulsating stars. They specialize in Telescope Operations Planning for astronomical observatories and publishing within Astrophysics and Astronomy literature. Recommendations will be used by research leads and telescope operators to better allocate research team and observatory resources. Insights are delivered to Research and Project managers. 

### Project Goals
  1. Object Segmentation and Profiling: To partition stars, and their observational data, into groups to based on location data, physical parameters, and pulsation data to expidite the search for candidate stars for further study. Determine which locations contain the most stars that have not been published in scientific literature?
  2. Pulsation Cohorts and Emergent Patterns: To detmermine relationships between the physical parameters of a star and its pulsation data in order to equip research teams performing variable star searches with heuristics that guide and expidite their processes.

## Data Overview
### Data Pipeline/ETL Process
The data is sourced from two different locations: ~84,000 rows (stars) from the TESS Variability Catalog (published by the American Astronomical Society in 2024: https://iopscience.iop.org/article/10.3847/1538-4365/acdee5), and an additional ~1,000 rows (stars) from my own pulsating star search of sectors 61-68 of TESS data which was matched with corresponding physical parameter data (Temperature, Mass, Radius, etc.) from the TICv8 catalog (via SQL join on unique star identifier). The whole of the data was migrated from .csv files to a MySQL database that I created where only the most relevant fields were stored in a flat file. The data was then cleaned in MySQL Workbench using data manipulation language. Finally, the flat file was loaded into Power BI using an ODBC connector where it was transformed into a star schema.
### Data Structure Overview
The data is comprised of several key aspects of interest to our researchers:
  1. Pulsation data: details whether a star has an identified pulsation, the period of the pulsation, and other characteristics associated with the strength, nature, and confidence level of the pulsation. Why relevant?
  2. Physical Parameters: data describing the stellar structure of stars; measures of physical properties such as surface temperature, mass, radius, etc. Why relevant?
  3. Location Data: details the location of stars in the sky – attributes such as celestial coordinates, distance from observer, and indicators of whether the an object's position will change over time. Why relevant?
  4. Stellar Classifications: contains descriptors from the data sources that suggest what class/type of star a given object is, and from what instrument the classification comes from. Provides useful groupings by which researchers can analyze subsets of the data. 

## Executive Summary
30 second take away with key insights...

## Insights Deep-Dive
### What parts of the sky have the lowest percentage of unpublished stars?

### What periods should we expect when looking at stars? Different classes?

### Affect of confidence levels on pulsation data

## Recommendations

## Clarifying Questions, Assumptions, and Caveats
### Questions for Stakeholders Prior to Project Advancement
### Assumptions and Caveats

Contents:
TESS Variable Catalog Analysis
  Project Background (ARDASTELLA intro, and what im doing – insights to expidite variable star study)
  Executive Summary (Detail data set, show data model, and ARDASTELLA dataset contributions. Seeking hueristics that govern variable star searches, saving resources i.e. money, telescope observation time, etc.)
  Insights Deep-Dive (no text here – straigh to the insights. Focus on metrics and tie things together.)
    insight 1. What stars are most likely to be variable?
    insight 2  What Periods should we expect when looking at stars? For different classes?
    insight 3  Confidence levels reveal trends in pulsation data?
  Recommendations (Guide the research team based on the insights above)
  Clarifying Questions, Assumptions, and Caveats
    Questions for Stakeholders Prior to Project Advancement
    Assumptions and Caveats
