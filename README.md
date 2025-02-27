# TESS Stellar Variability Catalog Analysis @ ARDASTELLA
![Ardastella_logo](https://github.com/user-attachments/assets/9b2b480b-0743-43da-a0c6-7212f9db9e1a)
## Background and Overview
ARDASTELLA is a research group consisting of University faculty, PhD students, and international collaborators working on pulsating stars. They specialize in Telescope Operations Planning for astronomical observatories and publishing within Astrophysics and Astronomy literature. Recommendations will be used by research leads and telescope operators to better allocate research team and observatory resources. Insights are delivered to Research and Project managers. 

### Project Goals
  1. Object profiling: To partition stars, and their observational data, into groups to based on location data, physical parameters, and pulsation data to expidite the search for candidate stars for further study. Determine which locations contain the most stars that have not been published in scientific literature?
  2. Pulsation Cohorts and Emergent Patterns: To detmermine correlations between the physical parameters of a star and its pulsation data. Variable star searches within large volumes of data is very time consuming. We aim to equip research teams with heuristics derived from analysis that will inform and expedite their variable star searches. 

## Data Overview
### Data Pipeline/ETL Process
The data is sourced from two different locations: ~84,000 rows (stars) from the TESS Variability Catalog ([published by the American Astronomical Society in 2024](https://iopscience.iop.org/article/10.3847/1538-4365/acdee5)), and an additional ~1,000 rows (stars) from my own pulsating star search of sectors 61-68 of TESS data which was matched with corresponding physical parameter data (Temperature, Mass, Radius, etc.) from the TICv8 catalog (via SQL join on unique star identifier). The whole of the data was migrated from .csv files to a MySQL database that I created where only the most relevant fields were stored in a flat file. The data was then cleaned in MySQL Workbench using data manipulation language. Finally, the flat file was loaded into Power BI using an ODBC connector where it was transformed into a star schema.
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

### Pulsation Period Distribution and Filtering; _Where should we look for pulsations?_
Below is a histogram counting the frequency of pulsation periods across the entire data set with no filters applied:
<p align="center">
  <img src="https://github.com/user-attachments/assets/15097f5a-18ed-4032-8a69-d5f978cd4bdc" alt="Period Distribution">
</p>
This visualization indicates a bi-modal distribution; there are two periods that occur most often – ~0.05 days and ~1.0 days. Additionally, there is a significant drop off in detected periods after ~1.10 days. If we begin slicing the data by attributes such as Confidence Level, Spectral Type, and Spectral Designation, we can determine what kinds of stars/stellar structure contributes to various period ranges.
<br/><br/>

  **1a. Slicing by Confidence Level: _High Confidence_** CONFIDENCE MATTERS
  
  In asterosiesmology, noise in your data is a fact of life. Effects such as photon noise (variance intrinsic to light), light from background sky, and noise contributions from the telescope itself, can give rise to signal in a periodogram where, in reality, there is no pulsation. Therefore, asterosiesmologists enforce a detection threshold which helps weed out noise from likely pulsations. The TESS Variability Catalog uses a metric called Power to quantify the strength of a signal. The threshold for a signal to be counted as a pulsation is 0.01 Power, however, pulsations above said threshold are split into High Confidence (> 0.1 Power) and Moderate Confidence (< 0.1 Power) categories. Below is the result when slicing by High Confidence:

![dashboard_all_HC](https://github.com/user-attachments/assets/5e1b9079-3f87-4e61-af62-6f0f31d7e56b)
> Hertzsprung-Russell Diagram: one of the most important visuals in Astronomy. It allows the user to get a profile of a stellar population at a glance; cooler stars are redder, hotter stars are bluer. More technical users can determine sizes of stars from their location on the graph.

High confidence pulsations in the dataset predominantly occupy the very short period range of ~0.05 days. These pulsations appear very strongly in their respective periodograms, with an average amplitude in the magnitude of tens of thousands, and an average Power of ~40 times the detection threshold. ???Additionally, as we cross highlight the histogram by Spectral Type, it can be seen that A stars contribute to this peak immensely, and F stars contribute to this peak significantly. The high confidence pulsations among the other spectral types are distributed more uniformly.
<br/><br/>

**1b. Slicing by Confidence Level: _Moderate Confidence_**

The frequency of moderate confidence pulsations increases until periods of ~1.10 days, at which point frequency decreases sharply and continues a shallow downward trend. A spike is evident at a period of 1.00 days. The average amplitude is the the magnitude of hundreds, and the average power, while still well above the detection threshold, is much closer to the boundary.
![dashboard_all_MC](https://github.com/user-attachments/assets/095750a7-5bd5-4e7f-8766-613c0655a8c0)

The population profiles of both categories are similar; the small changes in spectral type distribution cannot be responsible for such a drastic change in mode pulsation. Rather, it is more likely that lower confidence is an intrinsic property of longer period pulsations????



> Spectral type and HR diagram context
<br/><br/>

**2a. Filtering by Spectral Designation: _DWARF_**
![Dwarf_all_stars](https://github.com/user-attachments/assets/8c98e116-1b4a-4d77-a2c9-e4858b776d65)
<br/><br/>

**2b. Filtering by Spectral Designation: _GIANT_**
![Giant_all_stars](https://github.com/user-attachments/assets/f502c944-44e8-4761-a739-a3e043f8232b)
<br/><br/>

### Affect of confidence levels on pulsation data


![LC_all_stars-MadewithClipchamp-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/db888ea8-6a06-43a2-ab89-eda7e95973e6)

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

      **1a. Slicing by Confidence Level: _High Confidence_** CONFIDENCE MATTERS
  
  In asterosiesmology, data is noisey. Effects such as photon noise (variance intrinsic to light), light from background sky, and noise contributions from the telescope itself, can give rise to signal in a periodogram where, in reality, there is no pulsation. Therefore, asterosiesmologists enforce a detection threshold which helps weed out noise from likely pulsations. The TESS Variability Catalog uses a metric called Power to quantify the strength of a signal. The threshold for a signal to be counted as a pulsation is 0.01 Power, however, pulsations above said threshold are split into High Confidence (> 0.1 Power) and Moderate Confidence (< 0.1 Power) categories. Below is the result when slicing by High Confidence:
<p align="center">
  <img src="https://github.com/user-attachments/assets/5c5d310f-af4f-4dcd-b096-fe492e3f3af3">
</p>    
High confidence pulsations in the dataset predominantly occupy the very short period range of ~0.05 days. Additionally, as we cross highlight the histogram by Spectral Type, it can be seen that A stars contribute to this peak immensely, and F stars contribute to this peak significantly. The high confidence pulsations among the other spectral types are distributed more uniformly.
<br/><br/>

**1b. Slicing by Confidence Level: _Moderate Confidence_**

The frequency of moderate confidence pulsations increases until periods of ~1.10 days, at which point frequency decreases sharply and continues a shallow downward trend. A spike is evident at a period of 1.00 days. All spectral types, except for A type stars, exhibit a maximum frequency spike at a period of 1.00 days. Instead, A type stars contribute a bump in periods < 0.1 days, much like their high confidence data. Two spectral types have additional features in their histograms: G type stars have frequency bumps around ~0.16 days and ~1.07 days, and M-type stars have a frequency bump near ~1.07 days as well.WHAT ABOUT G-type DWARF VS GIANT??? SURELY THAT IS RELEVANT FOR PULSATION INFERENCES ABOUT STELLAR STRUCTURE 
<p align="center">
  <img src="https://github.com/user-attachments/assets/db888ea8-6a06-43a2-ab89-eda7e95973e6">
</p>    
> Spectral type and HR diagram context
<br/><br/>

**2a. Filtering by Spectral Designation: _DWARF_**
![Dwarf_all_stars](https://github.com/user-attachments/assets/8c98e116-1b4a-4d77-a2c9-e4858b776d65)
<br/><br/>

**2b. Filtering by Spectral Designation: _GIANT_**
![Giant_all_stars](https://github.com/user-attachments/assets/f502c944-44e8-4761-a739-a3e043f8232b)
<br/><br/>

### Affect of confidence levels on pulsation data


![LC_all_stars-MadewithClipchamp-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/db888ea8-6a06-43a2-ab89-eda7e95973e6)
