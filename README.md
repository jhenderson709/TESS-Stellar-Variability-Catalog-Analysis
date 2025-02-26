# TESS Stellar Variability Catalog Analysis @ ARDASTELLA
![Ardastella_logo](https://github.com/user-attachments/assets/9b2b480b-0743-43da-a0c6-7212f9db9e1a)
## Background and Overview
ARDASTELLA is a research group consisting of University faculty, PhD students, and international collaborators working on pulsating stars. They specialize in Telescope Operations Planning for astronomical observatories and publishing within Astrophysics and Astronomy literature. Recommendations will be used by research leads and telescope operators to better allocate research team and observatory resources. Insights are delivered to Research and Project managers. 

### Project Goals
  1. Object Segmentation and Profiling: To partition stars, and their observational data, into groups to based on location data, physical parameters, and pulsation data to expidite the search for candidate stars for further study. Determine which locations contain the most stars that have not been published in scientific literature?
  2. Pulsation Cohorts and Emergent Patterns: To detmermine relationships between the physical parameters of a star and its pulsation data. Variable star searches within large volumes of data is very time consuming. We aim to equip research teams with heuristics derived from analysis that will inform and expedite their variable star searches. 

## Data Overview
### Data Pipeline/ETL Process
The data is sourced from two different locations: ~84,000 rows (stars) from the TESS Variability Catalog (published by the American Astronomical Society in 2024: https://iopscience.iop.org/article/10.3847/1538-4365/acdee5), and an additional ~1,000 rows (stars) from my own pulsating star search of sectors 61-68 of TESS data which was matched with corresponding physical parameter data (Temperature, Mass, Radius, etc.) from the TICv8 catalog (via SQL join on unique star identifier). The whole of the data was migrated from .csv files to a MySQL database that I created where only the most relevant fields were stored in a flat file. The data was then cleaned in MySQL Workbench using data manipulation language. Finally, the flat file was loaded into Power BI using an ODBC connector where it was transformed into a star schema.
### Data Structure Overview
The data is comprised of several key aspects of interest to our researchers:
  1. Pulsation data: details whether a star has been attributed an identified pulsation, the period of the pulsation, and other characteristics associated with the strength, cause, and confidence level of the pulsation. Why relevant?
  2. Physical Parameters: data describing the stellar structure of stars; measures of physical properties such as surface temperature, mass, radius, etc. Why relevant?
  3. Location Data: details the location of stars in the sky – attributes such as celestial coordinates, distance from observer, and indicators of whether the an object's position will change over time. Why relevant?
  4. Stellar Classifications: contains descriptors from the data sources that suggest what class/type of star a given object is, and from what instrument the classification comes from. Provides useful groupings by which researchers can analyze subsets of the data. 

## Executive Summary
30 second take away with key insights...

## Insights Deep-Dive
### What parts of the sky have the lowest percentage of unpublished stars?

### What periods should we expect when looking at stars? Different classes?
Below is a histogram counting the frequency of pulsation periods across the entire data set with no filters applied:
<p align="center">
  <img src="https://github.com/user-attachments/assets/15097f5a-18ed-4032-8a69-d5f978cd4bdc" alt="Period Distribution">
</p>
This visualization indicates a bi-modal distribution; there are two periods that occur most often – ~0.05 days and ~1.0 days. Additionally, there is a significant drop off in detected periods after ~1.10 days. If we begin slicing the data by attributes such as Confidence Level, Spectral Type, and Spectral Designation, we can determine waht kinds of stars are contributing to the modes seen in the aforementioned histogram. 
<br/><br/>

  **1a. Slicing by Confidence Level: _High Confidence_** In asterosiesmology, data is noisey. Effects such as photon noise (variance intrinsic to light), light from background sky, and noise contributions from the telescope itself, can give rise to signal in a periodogram where, in reality, there is no pulsation. Therefore, asterosiesmologists enforce a detection threshold which helps weed out noise from likely pulsations. The TESS Variability Catalog uses a metric called Power to quantify the strength of a signal. The threshold for a signal to be counted as a pulsation is 0.01 Power, however, pulsations above said threshold are split into High Confidence (> 0.1 Power) and Low Confidence (< 0.1 Power) categories. Below is the result when slicing by High Confidence:
    
![dashboard_all_HC](https://github.com/user-attachments/assets/8a22b510-81e6-4e61-a082-2c427893b533)
High confidence pulsations in the dataset predominantly occupy the very short period range of ~0.05 days. Additionally, as we cross highlight the histogram by Spectral Type, it can be seen that A stars contribute to this peak immensely, and F stars contribute to this peak significantly. The high confidence pulsations among the other spectral types are distributed more uniformly.

> Spectral type and HR diagram context
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
