# TESS Stellar Variability Catalog Analysis @ ARDASTELLA
## Table of Contents
- [Background and Overview](#background-and-overview)
  - [TESS Background](#tess-background-what-is-tess-and-how-does-it-collect-data)
  - [Asteroseismology](#asteroseismology)
  - [Project Goals](#project-goals)
- [Data Overview](#data-overview)
  - [Data Pipeline/ETL Process](#data-pipelineetl-process)
  - [Data Structure Overview](#data-structure-overview)
- [Executive Summary](#executive-summary)
- [Insights Deep-Dive](#insights-deep-dive)
  - [Published/Unpublished Stars](#where-should-researchers-look-for-candidate-stars-for-academic-papers)
  - [Pulsations](#pulsation-period-distribution-and-filtering-where-should-we-look-for-pulsations)

    

# TESS Stellar Variability Catalog Analysis @ ARDASTELLA
![Ardastella_logo](https://github.com/user-attachments/assets/9b2b480b-0743-43da-a0c6-7212f9db9e1a)
## Background and Overview
  ARDASTELLA is a research group consisting of University faculty, PhD students, and international collaborators working on pulsating stars. They specialize in Telescope Operations Planning for astronomical observatories and publishing within Astrophysics and Astronomy literature. Recommendations will be used by research leads and telescope operators to better allocate research team and observatory resources. Insights are delivered to team members and research leads. 
<br/><br/>

##
### TESS Background; What is TESS, and how does it collect data?

The Transiting Exoplanet Survey Satellite (TESS) is a space telescope in Earth's orbit that has been a prolific source of astronomical data since its launch in 2018. While ostensibly intended for the discovery of exoplanets, its collection of time-series photometric data has been a valuable asset to scholars of stellar pulsations – asteroseismologists – following the retirement of the Kepler space telescope. TESS has four identical 24x24 degree field of view cameras that are ordered in such a way to form a composite 24x96 degree field of view. This 24x96 degree slice of sky is called a sector. Each ecliptic hemisphere of the sky is composed of 13 adjacent and partially overlapping sectors. To collect data, TESS is pointed at one sector and observes it (almost) continuously with various sampling rates for 27.4 days before it is directed at the next adjacent sector. The 13 sector survey takes a year to complete, after which the telescope shifts its field of view to the opposite hemisphere for observation of another series of 13 sectors. When both ecliptic hemispheres have been surveyed, TESS shifts its field of view again to the previously observed hemisphere at which point it will take new data of previously observed sectors. If a sector is called sector 1 when TESS observes it for the first time, when the telescope returns to that sector in its respective hemisphere two years later, it will be called sector 27.
<p align="center">
  <img src="https://github.com/user-attachments/assets/28a09eff-b35e-40c0-ae1f-7cfb85d89d0b">
</p>

> A demonstration of how TESS samples the night sky using data from the the TESS Variable Star Catalog. Each frame represents one sector of data from TESS' point of view. Note how the sectors flip from one hemisphere to the other – this change represents a new year of observations.


The TESS Variable Star Catalog worked to identify as many variable stars as possible within the first two years of TESS observations. Because TESS takes two years to complete its 'all-sky' survey cycle, we have access to most all known variable stars observed by TESS in our data set. The visualization below is configured to show all TESS VSC data for the first two years of the mission concurrently:
<p align="center">
  <img src="https://github.com/user-attachments/assets/1dbb5a90-880f-471f-bc18-d7ba3c580af6">
</p>

> This graph, and the one above it, are Mollweide projections – a way of drawing the entire surface of a round object, like Earth or the night sky, onto a flat oval shape. In this case, I have taken equatorial coordinates (Right Ascension and Declination), which describe the location of objects in space on the celestial sphere, and performed numerous tranformations on them to plot them appropriately. _Note:_ due to the volume of data points (~85,000) Power BI is showing "a subset that defines the shape and the outliers".

The gray dots in the Mollweide plot are stars in the data set that have been mentioned in academic papers. Indigo/purple dots in the plot are stars that have not yet been mentioned in academic papers. These are the stars we are most interested in; if upon further study these stars reveal something new, interesting, or useful for existing mathematical models, an academic paper can be drafted about them. The blank curved gap inbetween hemispheres represents zones not viewed by TESS – while described as an "all-sky survey," in reality, only ~85% of the sky is observed in a two year cycle.
<br/><br/>

##
### Asteroseismology
"Asteroseismology is the determination of the interior structures of stars by using their oscillations as seismic waves" (Handler, G 2013). In other words, asteroseismology is the study of vibrations inside stars. Just like how earthquakes cause seismic waves to travel through the Earth, which scientists use to study our planet’s interior, similar waves travel through stars, revealing what’s happening beneath their surfaces. Think of a star like a musical instrument. When you pluck a guitar string or strike a drum, it vibrates at different frequencies, producing sound. These vibrations depend on the size, shape, and material of the instrument. In the same way, a star’s physical parameters–such as its size, temperature, and composition—affect the way it oscillates. Now, imagine you have a drum that, when struck, gently swells and gets louder, until a maximum, at which point, it shrinks and gets softer–this is more like a stellar pulsation, and the volume level is like the brightness of the star.
<p align="center">
  <img src="https://github.com/user-attachments/assets/2672ede9-659d-4ac0-9066-c3e2e8a69fc0">
</p>

> An exaggerated model of how stars can physically expand and contract, resulting in observable pulsations. This example utilizes [spherical harmonics](https://en.wikipedia.org/wiki/Spherical_harmonics), also known as n, l, m geometry, to model the oscillations [(.gif credit)](https://commons.wikimedia.org/wiki/File:Y_l4m2.gif).

Deriving stellar pulsations is made possible by identifying and analyzing variable light signatures in the time-series light data (light curves) of stars observed by high-end telescopes like TESS. If periodicity is present in a star's light curve, Fourier analysis (a mathematical transformation of time-series data) will reveal a corresponding amplitude peak–a pulsation candidate–in the amplitude-frequency domain; an amplitude peak represents a frequency at which the star's pulsations are most prominent. If a given peak is vetted for noise and contamination considerations and is determined to be of sufficient amplitude, the amplitude peak can be called a pulsation and the star to which it belongs can be distinguished as a variable star.

Though beyond the scope of this project, the ultimate function of pulsations should be mentioned: Physical parameters of a star, such as surface temperature, gravity, mass, and luminosity, experience some degree of instability. In the case of variable stars, this instability is related to pulsation period. Each pulsation period corresponds to a specific n, l, m geometry (spherical harmonics), allowing us to use these geometries to constrain free parameters—physical properties of the star that cannot be directly observed but can be inferred. These modes or patterns of oscillation are key to understanding the star’s internal structure. As we analyze the pulsation geometry for each mode detected, we narrow down the range of possible solutions for the star’s structure. Crucially, there is only one true stellar structure for a given object, and this work aims to bring us closer to identifying that structure for the stars discussed.
<br/><br/>

##
### Project Goals
  1. Object profiling: To partition stars and their observational data into meaningful groups based on location, physical parameters, and pulsation characteristics. The goal is to streamline the identification of promising candidate stars for further study. This involves determining which regions of the sky contain the largest concentrations of stars that have yet to be explored or published in scientific literature, thus enabling a more focused and efficient search for novel variable stars.
  2. Pulsation Cohorts and Emergent Patterns: To uncover correlations between a star’s physical parameters (such as mass, temperature, radius) and its pulsation characteristics (such as pulsation period, amplitude, and power). By analyzing these relationships, the project aims to provide research teams with data-driven heuristics that can significantly expedite the process of identifying variable stars within large datasets. This would reduce the time and effort required for variable star searches, particularly in massive datasets like those from TESS.
  3. Enhancing Understanding of TESS Observations: To equip users with a deeper intuition and understanding of how the TESS mission operates, including its observational strategies, limitations, and the types of data it provides. This will help researchers interpret TESS data more effectively and develop strategies for future observational campaigns.
<br/><br/>


## Data Overview
### Data Pipeline/ETL Process

  Nearly all of the data is sourced from a single location: within the Mikulski Archive for Space Telescopes (MAST) website, a popular resource for astronomy-astrophysics, a bulk .csv download is provided for the TESS Variable Star Catalog (TESS VSC), which was [published by the American Astronomical Society in 2023](https://iopscience.iop.org/article/10.3847/1538-4365/acdee5).

![TESS_SVC_csv](https://github.com/user-attachments/assets/d16d9cea-c39d-4293-9c75-801b7da5950e)

This file contains ~85,000 rows with well over 100 columns. Most of the data are numeric values describing physical parameters of stars, measurments describing observational conditions, or text fields helping to identify or denote various star types and data sources.

In order to start working with the data, I decided to load the .csv into a personal dedicated MySQL database. First, a table configured for only the most relevant fields was required (some fields were renamed for personal preference/clarity):

```sql
CREATE TABLE TESS_VSC_varchar_staging (
    TIC VARCHAR(50),
    catalog_name VARCHAR(50),
    stellar_class VARCHAR(50),
    sector_id VARCHAR(50),
    Teff VARCHAR(50),
    e_Teff VARCHAR(50),
    logg VARCHAR(50),
    e_logg VARCHAR(50),
    Rad VARCHAR(50),
    e_Rad VARCHAR(50),
    Mass VARCHAR(50),
    e_Mass VARCHAR(50),
    Dist VARCHAR(50),
    e_Dist VARCHAR(50),
    r_Teff VARCHAR(50),
    RAJ2000 VARCHAR(50),
    DEJ2000 VARCHAR(50),
    pmRA VARCHAR(50),
    e_pmRA VARCHAR(50),
    pmDE VARCHAR(50),
    e_pmDE VARCHAR(50),
    max_pulsation VARCHAR(50),
    amplitude_1 VARCHAR(50),
    power_1 VARCHAR(50)
);
```

Above is a raw staging table in which all data types are defined as VARCHAR. Given the variety of decimal precision, data types, and special characters, this preliminary stage allows for a quick hands-on approach by which the data can be profiled and better understood. 

With a staging table created, data from the aforementioned .csv could be loaded into the table in MySQL workbench:

```sql
LOAD DATA LOCAL INFILE 'C:\\Program Files\\MySQL\\MySQL Server 9.1\\Uploads\\TESS_VSC.csv'
INTO TABLE TESS_VSC_varchar_staging
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
IGNORE 1 LINES
(tess_id, Sector, period_var_1, amp_var_1, power_1, TWOMASS, objType, ra, `dec`, pmRA, e_pmRA, pmDEC, e_pmDEC, Teff, e_Teff, logg, e_logg, rad, e_rad, mass, e_mass, rho, e_rho);
```

Now the data could be cleaned; using data manipulation language, nan values were updated to be set equal to null, decimal places were truncated to desired precisions, REGEXP was used to remove undesired spaces and special characters, and some fields were transformed to be more workable. 

A second staging table was then implemented in the pipeline to appropriately define data types and act as a fail-safe, preserving a finalized version of the cleaned data:

```sql
CREATE TABLE TESS_VSC_datatype_staging AS
SELECT 
    CAST(TIC AS UNSIGNED INT) AS TIC,
    catalog_name,
    stellar_class,
    CAST(sector_id AS UNSIGNED INT) AS sector_id,
    CAST(Teff AS DECIMAL(10,1)) AS Teff,
    CAST(e_Teff AS DECIMAL(10,1)) AS e_Teff,
    CAST(logg AS DECIMAL(8,4)) AS logg,
    CAST(e_logg AS DECIMAL(8,4)) AS e_logg,
    CAST(Rad AS DECIMAL(10,3)) AS Rad,
    CAST(e_Rad AS DECIMAL(10,3)) AS e_Rad,
    CAST(Mass AS DECIMAL(10,3)) AS Mass,
    CAST(e_Mass AS DECIMAL(10,3)) AS e_Mass,
    CAST(Dist AS DECIMAL(10,4)) AS Dist,
    CAST(e_Dist AS DECIMAL(10,4)) AS e_Dist,
    r_Teff,
    CAST(RAJ2000 AS DECIMAL(20,11)) AS RAJ2000,
    CAST(DEJ2000 AS DECIMAL(20,11)) AS DEJ2000,
    CAST(pmRA AS DECIMAL(10,3)) AS pmRA,
    CAST(e_pmRA AS DECIMAL(10,3)) AS e_pmRA,
    CAST(pmDE AS DECIMAL(10,3)) AS pmDE,
    CAST(e_pmDE AS DECIMAL(10,3)) AS e_pmDE,
    CAST(max_pulsation AS DECIMAL(10,2)) AS max_pulsation,
    CAST(amplitude_1 AS DECIMAL(10,2)) AS amplitude_1,
    CAST(power_1 AS DECIMAL(10,3)) AS power_1
FROM TESS_VSC_varchar_staging;
```
With the data cleaned and structured, a production table was created to ensure data integrity and provide a stable dataset for analysis in Power BI. Unlike the staging tables, which facilitate transformation and validation, the production table serves as the final authoritative source for visualization and reporting:

```sql
CREATE TABLE TESS_VSC_production (
    TIC INT UNSIGNED,
    catalog_name VARCHAR(50),
    stellar_class VARCHAR(50),
    sector_id INT UNSIGNED,
    Teff DECIMAL(10,1),
    e_Teff DECIMAL(10,1),
    logg DECIMAL(8,4),
    e_logg DECIMAL(8,4),
    Rad DECIMAL(10,3),
    e_Rad DECIMAL(10,3),
    Mass DECIMAL(10,3),
    e_Mass DECIMAL(10,3),
    Dist DECIMAL(10,4),
    e_Dist DECIMAL(10,4),
    r_Teff VARCHAR(50),
    RAJ2000 DECIMAL(20,11),
    DEJ2000 DECIMAL(20,11),
    pmRA DECIMAL(10,3),
    e_pmRA DECIMAL(10,3),
    pmDE DECIMAL(10,3),
    e_pmDE DECIMAL(10,3),
    max_pulsation DECIMAL(10,2),
    amplitude_1 DECIMAL(10,2),
    power_1 DECIMAL(10,3),
    PRIMARY KEY (TIC, sector_id)
);
```

Finally, an INSERT statement is used to load the clean data into our production table:

```sql
INSERT INTO TESS_VSC_production
SELECT * FROM TESS_VSC_datatype_staging
```

The resultant flat file was loaded into Power BI using an ODBC connector where it was transformed into a star schema: In Power Query, reference tables were created from the source data and stripped down to fields pertaining to specific entities. To optimize performance, data redundancy was minimized by removing duplicate values, clustered indexes were created to improve query efficiency, and primary/foreign key relationships were established between tables to maintain referential integrity.

MENTIONED IN PAPER PYTHON SCRIPT?
<br/><br/>

##
### Data Structure Overview
The data is comprised of several key aspects of interest to our researchers:
  1. _Pulsation data:_ TESS VSC details whether a star has been attributed an identified pulsation, the period of the pulsation, and other characteristics associated with the strength, cause, and confidence level of the pulsation. Exploratory analysis of this data can reveal trends and patterns among similiar stars, and asteroseismic mode analysis of this data can help to constrain stellar models. 
  2. _Physical Parameters:_ This dataset includes key properties that describe the stellar structure, such as surface temperature (Teff), mass, radius, and luminosity, among others. These parameters are fundamental in understanding stellar evolution, classification, and behavior. The data's relevance lies in its ability to establish correlations between a star's physical properties and its pulsation characteristics.
  3. _Location Data:_ The location data provides essential information such as celestial coordinates (Right Ascension, Declination), the distance from Earth, and proper motion (pmRA, pmDE), which describe how stars are moving across the sky. This data is crucial for mapping the distribution of stars in TESS' field of view and understanding the dynamics of star populations. In this case, location data enables the identification of pulsating stars, and whether they have been published in academic papers, in specific regions of the sky, allowing for a more targeted study of variability and pulsation that could result in a new academic publication.
  4. _Stellar Classifications:_ This dataset includes descriptors that classify stars based on their observed characteristics, such as spectral type, luminosity class, and other classification schemes. The classifications help group stars with similar properties, enabling researchers to focus on specific subsets of the data that share common characteristics. For example, by analyzing pulsation behavior within specific stellar classes (e.g., white dwarfs or red giants), researchers can gain deeper insights into the mechanisms behind their variability. These classifications also provide information on the instrument used to obtain the data, which is important for understanding the potential limitations or biases introduced during observation.
     
![semantic_model_rework](https://github.com/user-attachments/assets/0dc5074b-09ae-416a-9af1-f286b095c9f6)
> A screenshot of the semantic model as it exists within Power BI.
<br/><br/>

##
## Executive Summary
Sector 19 from Year 2 of TESS VSC data has an 11.11% unpublished star population, making it a valuable resource for new research. Notably, 16% of DWARF stars in this sector remain unpublished, while GIANT star researchers may prefer Sectors 10 and 11, where 5% of GIANTS are unpublished.

For pulsation studies, DWARF stars cluster around ~0.05-day periods, while GIANTS peak at ~1.00 days. A-type DWARFs consistently exhibit ~0.03-day periods, whereas GIANTS show broader period distributions. M-type GIANTS are of particular interest due to their anomalous lack of short-period pulsations.
<br/><br/>


## Insights Deep-Dive
### Where should researchers look for candidate stars for academic papers?
In order to make best use of team resources, we want to direct attention to those sectors of the sky which have the highest percentages of unpublished stars. Once this has been determined, researchers will be recommended to said sectors to conduct period spacing searches on known variable stars(?). However, ideal sectors may vary depeding on one's research objectives. For example: where should one look if they are hoping to publish on stars within a specific year of TESS observations? What sector should one examine if they are focused on publishing on pulsating GIANT stars? Pulsating DWARF stars? The dynamic filtering functionality implemented into the below dashboards allow team members to answer these questions.
<br/><br/>

##
**1a. Slicing by Year: _Year 1_**

Year 1 observations comprise sector IDs 1 - 13. These sectors encompass the southern hemisphere of TESS' field of view:

![TESS_all_year1](https://github.com/user-attachments/assets/7838b5ae-aa91-49e3-ae13-fe98cdadb6f3)
* The top 5 sectors IDs in year 1 with the largest percentages of unpublished variable stars are as follows: 10 (9%), 7 (8%), 11 (7%), 6 (7%), 3 (7%).
* Year 1 observations contain the 3 most published sectors in the dataset; only 2% of sector 1 stars are unpublished verified variable stars, while sectors 13 and 4 have 4% and 5% respectively.
* While there are more unpublished stars within this data, their are fewer unpublished stars when compared to year 2 proportionally.
<br/><br/>

**1b. Slicing by Year: _Year 2_**

Year 2 observations comprise sector IDs 14 - 26. These sectors encompass the northern hemisphere of TESS' field of view:

![TESS_all_year2](https://github.com/user-attachments/assets/680286cd-983a-4632-965a-4affef644f17)
* The top 5 sectors IDs in year 2 with the largest percentages of unpublished variable stars are as follows: 19 (11%), 24 (10%), 18 (8%), 17 (7%), 16 (7%).
* Sector 19 has the highest percentage of unpublished variable stars across the whole data set: 11.11%
* Proportionally, Year 2 observations have a greater porportion of DWARF stars across all of its sectors when compared to Year 1.
<br/><br/>

##
**2a. Slicing by Spectral Designation: _DWARF_**

![TESS_DWARF_VSC](https://github.com/user-attachments/assets/ae246d66-49e0-4cdf-94f9-70862e5f2fdf)
* DWARF stars are common in the dataset – they account for 64% of stars in the catlog. 
* DWARF stars are much less published than giants
* Sector 19 DWARF stars are 16% unpublished!
<br/><br/>

**2b. Slicing by Spectral Designation: _GIANT_**

![TESS_GIANT_VSC](https://github.com/user-attachments/assets/c10545bd-1eb3-4cce-847d-fb486bdaebc7)
* GIANT stars are less common in any stellar population, and that proves true in the TESS VSC. 29% of stars in the data set are GIANT stars.
* GIANT stars within the data have been thouroughly examined. Many sectors have 99% of their GIANT stars featured in a publication already.
* Sector 10 has the highest percenatage of unpublished GIANT stars: 5%

##
### Pulsation Period Distribution and Filtering; _Where should we look for pulsations?_
Below is a histogram, constructed with a bin size of 0.01 days, counting the frequency of pulsation periods across the entire data set with no filters applied:
<p align="center">
  <img src="https://github.com/user-attachments/assets/7c377b2f-9286-485d-9512-f4afc472cf43">
</p>
This visualization indicates a bi-modal distribution; there are two periods that occur most often – ~0.05 days and ~1.0 days. Additionally, there is a significant drop off in detected periods after ~1.10 days. If we begin slicing the data by attributes such as Confidence Level, Spectral Type, and Spectral Designation, we can determine what kinds of stars/stellar structure contributes to various period ranges.
<br/><br/>

##
### Confidence Matters

  **1a. Slicing by Confidence Level: _High Confidence_**
  
  In asterosiesmology, noise in your data is inevitable. Effects such as photon noise (variance intrinsic to light), light from background sky, and noise contributions from the telescope itself, can give rise to signal in a periodogram where, in reality, there is no pulsation. Therefore, asterosiesmologists enforce a detection threshold which helps weed out noise from likely pulsations. The TESS Variability Catalog uses a metric called Power to quantify the strength of a signal. The threshold for a signal to be counted as a pulsation is 0.01 Power, however, pulsations above said threshold are split into High Confidence (> 0.1 Power) and Moderate Confidence (< 0.1 Power) categories. Below is the result when slicing by High Confidence:

![HC_all_new](https://github.com/user-attachments/assets/67502652-08ba-4717-989a-eeac816f595e)
> _Hertzsprung-Russell Diagram:_ one of the most important visuals in Astronomy. It allows the user to get a profile of a stellar population at a glance; cooler stars are redder, hotter stars are bluer. More technical users can determine sizes of stars from their location on the graph.
> _Spectral Type:_ organizes stars into groups based on their surface temperature. They rank O, B, A, F, G, K, M from hottest to coolest.
* High confidence pulsations in the dataset predominantly occupy the very short period range of ~0.05 days.
*  These pulsations appear very strongly in their respective periodograms, with an average amplitude in the magnitude of tens of thousands, and an average Power of ~40 times the detection threshold.
* ???Additionally, as we cross highlight the histogram by Spectral Type, it can be seen that A stars contribute to this peak immensely, and F stars contribute to this peak significantly. The high confidence pulsations among the other spectral types are distributed more uniformly.
<br/><br/>

**1b. Slicing by Confidence Level: _Moderate Confidence_**

  The frequency of moderate confidence pulsations increases until periods of ~1.10 days, at which point frequency decreases sharply and continues a shallow downward trend. A spike is evident at a period of 1.00 days. The average amplitude is the the magnitude of hundreds, and the average power, while still well above the detection threshold, is much closer to the boundary.

![MC_all_new](https://github.com/user-attachments/assets/6173700c-5e38-4b8c-ad02-475e3c8d87b3)
* The population profiles of both categories are similar; the small changes in spectral type distribution cannot be responsible for such a drastic change in mode pulsation. Rather, it is more likely that lower confidence is an intrinsic property of longer period pulsations????
<br/><br/>

##
### Pulsation modes correlate to physical parameters: _DWARF_

  This designation refers specifically to Main Sequence dwarfs. They range from O-type (blue i.e. hot, massive) to M-type (red i.e. cool, small) and they all fuse hydrogen to helium in their cores. Most stars in the universe are main sequence stars such as these, and by and large, they are on the cooler side. Below is a dashboard representing data for all dwarf stars in the data set:

![all_dwarf_new](https://github.com/user-attachments/assets/481bae3a-d8f2-4d4d-ba18-d2cca0e0068c)
<br/><br/>

##
**2a. Filtering by Spectral Type: _A-Type DWARF_**

  A-type dwarf stars have temperatures ranging from 7,300K - 10,000K. They are typically slightly more massive and have slightly larger radii than our sun, but are 5 to 25 times brighter. 

![A_dwarf_new](https://github.com/user-attachments/assets/aa733751-d0bd-4bf8-a261-6bb90562b95e)
* Regardless of confidence level, these stars output the vast majority of observed pulsation in the very short period region of ~0.05 days.
*  There are no other outstanding peaks in the period range, and beyond a period of 6 days, there are many bins in the histogram with 0 recorded pulsations.
*  Therefore, researchers conducting variable star searches of A-type dwarfs are advised to focus their efforts in the short period region to conserve resources. Additionally, team members are encouraged to investigate the near-monolithic nature of the pulsations – why do we not see the peak common around a period of 1.00 days, and what can this tell us about the structure of these stars?
<br/><br/>

**2b. Filtering by Spectral Type: _G-Type, K-Type DWARF_**

![G_K_dwarf_HC_new](https://github.com/user-attachments/assets/7522e7c1-9d14-408a-9212-e4240f06ed6d)
<br/><br/>

##
### Pulsation modes correlate to physical parameters: _GIANT_

  As main sequence dwarf stars fuse hydrogen into helium, they deplete the amount of hydrogen in their core. When hydrogen in the core runs out, the star begins to contract, heating its core. If temperatures in the core are sufficiently high (i.e. if the star is massive enough), the fusion of helium to carbon can begin. This fusion releases far more energy than hydrogen to helium fusion, causing the star to expand to 100 to 1,000 times its original size – a giant star is born. Giant stars can exist as any of the spectral types, but they are commonly found in the K and M temperature ranges. The below dashboard is configured to include data for all giant stars in the dataset.

![all_giant_new](https://github.com/user-attachments/assets/17224c57-dab6-4f22-8107-017d87fb7148)
> Notably, K-type stars make up 80% of the giant population in our data, so this data is largely skewed by contributions from K-type giants. 
* Features include a bump in pulsation count around a period of 0.37 days, a global maximum at 1.00 day, and a sharp decline in count at ~1.10 days. From that point on, frequency trends slightly downward until flattening out around a period of 6 days.
* Unlike the dwarfs in our sample, there is no spike in the very short period region. (what does this tell us about stellar structure; what inferences can be made?)
<br/><br/>

**3a. Filtering by Spectral Type: _High Confidence K-Type GIANT_**

K-type stars have a surface temperatures from 3,900K - 5,300K. Giant stars of this type are 

![K_giant_HC_new](https://github.com/user-attachments/assets/4abb1060-18e2-47e2-8903-a2de7642ecc2)
* High confidence pulsations for K-type giants are somewhat evenly spread across the period range, however, there is a significant bias for periods in the range of ~0.50 to ~6.00 days.
* Features in the histogram include a frequency peak at 1.05 days, a steep incline in count around 0.75 days, and a local peak in an otherwise relatively inactive region at a period of 0.15 days.
* The intensity of these pulsations are diminished when compared to high confidence data in the rest of the data set – average amplitude for these stars are ~6,000 ppt, and average Power is 0.33.
<br/><br/>

**3b. Filtering by Spectral Type: _Moderate Confidence K-Type GIANT_**

Moderate confidence data for these stars reveal a different story:

![K_giant_MC_new](https://github.com/user-attachments/assets/381f42b1-f508-4567-9cc2-59f3ce5d948e)
* Most all of the pulsations are consolidated in a period range < ~1.50 days. Beyond this point, there are no pulsations with a frequency of 25, and count continues to taper off until expected values are 1 or 0.
* Additionally, these pulsations are faint – amplitudes are only ~200 ppt on average and average power is only 4 times the detection threshold.
* Power and amplitude diminution are generally evident in giants, but it is especially true for K-types. In fact, they have the lowest pulsation amplitudes and power measurements for any of the spectral designations included in the data. These stars are large, more luminous than dwarves, but warmer than red giants, so why is it that these parameters read lower than all dwarf stars, but higher than red giants?
<br/><br/>

**3c. Filtering by Spectral Type: _M-Type GIANT_**

  M-type stars are the coolest of the classes defined by the Harvard system with surface temperatures ranging from 2,300K - 3,900K. They are typically stars of average or intermediate mass (1-8 solar masses) and are the second most common type of giant star. The histogram for this group of stars is perhaps the most distinctive of the data set:

![M_giant_HC_new](https://github.com/user-attachments/assets/a3a687ee-775a-4729-9138-a1e43ea5a87a)
* There are almost no pulsations under a period of ~3 days, except for a small local peak at a period of 1.00 days.
* The bulk of the pulsations are spread throughout the latter 3/4 of the period spectrum, with a global maxiumum at a period of 9.66 days.
* What is it about these stars that results in such a volume of long period pulsations? What might this tell us about stellar structure?
<br/><br/>

## Recommendations

## Clarifying Questions, Assumptions, and Caveats
Why are there more stars in year 1 than year 2?
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

