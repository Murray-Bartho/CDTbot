# DPOAE-Analyzer
This program takes user bias out of Distorted Product Otoacoustic Emission (DPOAE) data analysis. Previously, DPOAEs were "called" by eye, with a best guess. With DPOAE Analyzer, that uncertainty goes out the window. Be confidant in the statistical power of your DPOAE analysis with DPOAE Analyzer!


## High Level Overview
Essentially, the Analyzer averages the values on either side of the potential Distorted Product (DP) value to create a "noise floor." Then, it compares the height of the DP to the noise floor, to determine statistical significance! Simply load the .csv file generated by BioSigRZ into the app, and hit "Run" to see whether the DP is significant or not for each dB/frequency combination. 

## How to Use
Detailed step-by-step operations instructions, with images, can be found at: 

### Plain Text Instructions: 
1. Select the desired testing signals in BioSigRZ. This can be done by selecting History > Access Record File.
2. Once the BioSigRZ screen populates with the signals, select as many as you would like to analyze. 
3. History > Export to .csv
4. Open DPOAE Analyzer
5. Import File > navigate to the .csv you just created. Click "Save."
6. Run!
7. If you would like to save your results, select "Download" and then select a location for the program to download an .xlsx file to. 

## Installation
Detailed step-by-step installation instructions can be found in the Matlab Runtime Readme.txt included in the download files. 

To download, download the MATLAB app installer and follow the command prompts. If you do not have MATLAB Runtime previously installed, expect the download to take slightly longer (~5 mins). Make sure to tick the "Create Desktop Shortcut" box for easy access. 

## Detailed Code Explanation
The code analyses the .csv file provided by BioSigRZ. In said .csv file, there are 2048 columns of acoustic data, going from 0 hz to 97656.3 hz. The bin size of each data column is then determined by dividing the total frequency (97656.3) by the number of columns (2048). The .csv file also gives the hz at which the DP will be located at for each frequency. That value is then divided by the bin size, and rounded to the nearest whole number, to arrive at the column of the given DP. Then, 10 values from either side of the DP, not including the 2 values directly adjacent to the DP, are averaged to create the noise floor. The standard deviation of these 20 values is also calculated. If the DP value is 2 times greater than or equal to the standard deviation above the noise floor (>= ((2*std.dev.)+ noise floor average)), then the DP is considered statistically significant, and assigned a value of 1. If this threshold is not met, the DP is not considered statistically significant, and is assigned a value of 0.

The majority of the rest of the raw code deals with GUI design, handling user input error, and fiddling with MATLAB's labrynthine data type conversions. Raw code can be found linked below. 

## Known Bugs and Errors
- RemoveSheet123 does not work on Mac systems. The default 3 sheets will precede the Data and Metadata sheets on Mac. Fix will be implemented when the Stanford CSBF releases the MATLAB 2019b licence to its users. Matlab 2019b does not create the default 3 sheets on Excel when using writetable() or writecell(), eliminating the need for the RemoveSheet123 function. 

## Motivation
The Core Facilities team was pondering how to quickly and accurately determine DP when the possibility of a statistical package was tossed around. After a week of proof-of-concept testing, app development began in earnest. We are motivated to reduce user bias in DPOAE data analysis, as well as saving hard-working scientists around the world some time. 

## Build Status
Development Begins - November 2019

Beta Testing - December 2019

GitHub First Commit - January 2020

## Contribute
Please email all bugs / content suggestions / improvements to mbartho@stanford.edu. Thank you for your help! 

If you used this program in your research, please cite it! We would love nothing more than to see it used out in the wild. 

## Source Code
Source code can be found at: 

## Credits
### Dev Team:
	Murray Bartho
	Patrick Atkinson, Ph.D.
	Anthony Ricci, Ph.D.

### Functions Used:
	Noam Greenboim (2019). RemoveSheet123 - remove default Excel sheets (https://www.mathworks.com/matlabcentral/fileexchange/50371-			removesheet123-remove-default-excel-sheets), MATLAB Central File Exchange. Retrieved December 9, 2019.

### Funding:
	Stanford University School of Medicine: Department of Otolaryngology - Head & Neck Surgery
	Stanford Initiative to Cure Hearing Loss (SICHL)

### Acknowledgements:
	MathWorks and MATLAB
	Stanford Computational Services and Bioinformatics Facility (CSBF)
	Iconsflow.com

## Licenses
MATLAB by Mathworks 2009b, 2010a and 2019a were used in the development of this application. 
MATLAB licensing was acquired through the academic institutional license provided by Stanford CSBF. 

FREE Icon Maker by Iconsflow.com was used to develop the app icon. 
The free subscription plan was used to develop the Headphone Mouse icon, to be used in non-commercial academic research or other not-for-profit scholarly purposes. 

This program is protected by the MIT License, copied from Choose A License: https://choosealicense.com/licenses/mit/

