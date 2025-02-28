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
Below is a histogram, constructed with a bin size of 0.01 days, counting the frequency of pulsation periods across the entire data set with no filters applied:
<p align="center">
  <img src="https://github.com/user-attachments/assets/7c377b2f-9286-485d-9512-f4afc472cf43">
</p>
This visualization indicates a bi-modal distribution; there are two periods that occur most often – ~0.05 days and ~1.0 days. Additionally, there is a significant drop off in detected periods after ~1.10 days. If we begin slicing the data by attributes such as Confidence Level, Spectral Type, and Spectral Designation, we can determine what kinds of stars/stellar structure contributes to various period ranges.
<br/><br/>

  **1a. Slicing by Confidence Level: _High Confidence_** CONFIDENCE MATTERS
  
  In asterosiesmology, noise in your data is a fact of life. Effects such as photon noise (variance intrinsic to light), light from background sky, and noise contributions from the telescope itself, can give rise to signal in a periodogram where, in reality, there is no pulsation. Therefore, asterosiesmologists enforce a detection threshold which helps weed out noise from likely pulsations. The TESS Variability Catalog uses a metric called Power to quantify the strength of a signal. The threshold for a signal to be counted as a pulsation is 0.01 Power, however, pulsations above said threshold are split into High Confidence (> 0.1 Power) and Moderate Confidence (< 0.1 Power) categories. Below is the result when slicing by High Confidence:

![HC_all](https://github.com/user-attachments/assets/9751f785-d30c-4fe2-a39b-27643d4d734e)
> _Hertzsprung-Russell Diagram:_ one of the most important visuals in Astronomy. It allows the user to get a profile of a stellar population at a glance; cooler stars are redder, hotter stars are bluer. More technical users can determine sizes of stars from their location on the graph.
> _Spectral Type:_ organizes stars into groups based on their surface temperature. They rank O, B, A, F, G, K, M from hottest to coolest.

High confidence pulsations in the dataset predominantly occupy the very short period range of ~0.05 days. These pulsations appear very strongly in their respective periodograms, with an average amplitude in the magnitude of tens of thousands, and an average Power of ~40 times the detection threshold. ???Additionally, as we cross highlight the histogram by Spectral Type, it can be seen that A stars contribute to this peak immensely, and F stars contribute to this peak significantly. The high confidence pulsations among the other spectral types are distributed more uniformly.
<br/><br/>

**1b. Slicing by Confidence Level: _Moderate Confidence_**

The frequency of moderate confidence pulsations increases until periods of ~1.10 days, at which point frequency decreases sharply and continues a shallow downward trend. A spike is evident at a period of 1.00 days. The average amplitude is the the magnitude of hundreds, and the average power, while still well above the detection threshold, is much closer to the boundary.

![MC_all](https://github.com/user-attachments/assets/871efcd3-fcff-4a12-b803-31bfaa4f8248)

The population profiles of both categories are similar; the small changes in spectral type distribution cannot be responsible for such a drastic change in mode pulsation. Rather, it is more likely that lower confidence is an intrinsic property of longer period pulsations????



<br/><br/>

**2a. Filtering by Spectral Designation: _DWARF_**

This designation refers specifically to Main Sequence dwarfs – they range from O-type (blue i.e. hot, massive) to M-type (red i.e. cool, small) stars that fuse hydrogen to helium in their cores. Most stars in the universe are main sequence stars such as these, and by and large, they are on the cooler side.

![Dwarf_all](https://github.com/user-attachments/assets/0479dc0b-5c09-4586-9500-0ab6b7232fa0)
<br/><br/>

A-type dwarf stars have temperatures ranging from 7,300K - 10,000K. They are typically slightly more massive and have slightly larger radii than our sun, but are 5 to 25 times brighter. 

![A_all_dwarf](https://github.com/user-attachments/assets/d3c558f7-edbc-45fc-ad7b-4bd2abb156bb)
<br/><br/>
Interestingly, regardless of confidence level, these stars output the vast majority of observed pulsation periods in the very short period region of ~0.05 days. There are no other outstanding peaks in the period range, and beyond a period of 6 days, there are many bins in the histogram with 0 recorded pulsations. Therefore, researchers conducting variable star searches of A-type dwarfs are advised to focus their efforts in the short period region to conserve resources. Additionally, team members are encouraged to investigate the near-monolithic nature of the pulsations – why do we not see the peak common around a period of 1.00 days, and what can this tell us about the structure of these stars?

![G_K_HC_dwarf](https://github.com/user-attachments/assets/984c3b9d-24d8-484e-a458-00bd4b938b53)
<br/><br/>

**2b. Filtering by Spectral Designation: _GIANT_**

![Giant_all](https://github.com/user-attachments/assets/05560868-c31b-4a6c-8e98-b04c94d96cef)
<br/><br/>

![K_HC_giant](https://github.com/user-attachments/assets/b9f6c9d3-f7e5-4a9b-872a-5fb9ef063f2f)
<br/><br/>

![K_MC_giant](https://github.com/user-attachments/assets/115ce025-88a6-4c6c-9790-3ce5416f6502)
<br/><br/>

![M_HC_giant](https://github.com/user-attachments/assets/0eccc805-9541-4890-8ae5-6432890ea09c)
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
