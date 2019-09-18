# Hydrolight53_Bootstrap
HE53_Bootstrap enables user to evaluate radiative transfer using field-measured inherent optical properties (IOPs).  The program accepts ac-s and hs6 data and performs bootstrapping with replacement to produce a series of depth-binned absorption, attenuation, and backscattering spectra. The resulting output files can be uploaded into Hydrolight for modeling radiative transfer.

This python notebook ingests field-sampled IOPs (absorption, attenuation, and backscattering), and performs bootstrapping with replacement within user-specified depth-bins. Hydrolight53_Bootstrap then outputs bootstrapped, depth-binned IOPs into Hydrolight-compatible ascii files. User specifies the number of bootstrapping iterations. It is designed primarily for absorption/attenuation and backscattering data sampled with WET Labs (Seabird Scientific) ac-s meter and HOBI Labs Hydroscat-6 (hs6). Although not tested with Hydroscat-4 and Hydroscat-2, I am reasonably confident that Hydrolight53_Bootstrap will work with these platforms as well. Prior to use, data should be processed using acsPROCESS_INTERACTIVE/acsPROCESS_SEABASS (ac-s) or hs6PROCESS_INTERACTIVE/hs6PROCESS_SEABASS. We are also reasonably confident however, that this code is also compatible with much of the absorption/attenuation and particulate backscattering data posted on NASA's SeaBaSS database. Bootstrapping protocols are described in Bausell et al. (2019).

Hydrolight53_Bootstrap was written for use on a mac, but assuming that users will run Hydrolight on a pc. However, should this not be the case, code should be easily alterable to remedy this issue (I apologize for not getting around to it myself). Once the program is initiated, user is prompted to select an input file in which he/she has previously stated settings for running Hydrolight. We describe this file below and include template (Hydrolight53_Bootstrap_UserTemplate.txt) to assist the user.

Hydrolight53_Bootstrap produces three types of outputs: 
  1. Hydrolight-compabible bootstrapped absorption/attenutation files
  2. Hydrolight-compabible bootstrapped backscattering files, 
  3. Hydroligth batch files used for running these data and completing radiative transfer
  
Each bootstrapping iteration produces a triplet of the above-mentioned files, which are sorted in three folders and placed in the same pathway as the field-sampled ac-s data. Before running Hydrolight, these folders (along with field-sampled above-water solar irradiance) should be moved mannually into the appropriate pathways as indicated by batch files so that Hydrolight can locate them. 

Hydrolight53_Bootstrap creates Hydrolight batch files with a combination of fixed, and user-specified settings. 
Fixed settings include:
	1. User-supplied absorption/attenuation and particulate backscattering files (mentioned above)
	2. Forand-Fournier Phase Function
	3. Chlorophyll Fluorescence Included.  
		Chlorophyll is constant with depth
		Chlorophyll-based model for Cast 1 water
	4. CDOM Fluorescence Excluded
	5. Raman Scattering Excluded
	6. Real Index of refraction (n = -1.34)
	7. Solar Irradiance - semi-empirical sky model w/ user-supplied irradiances
	8. Seafloor - infinitely deep
	9. User-supplied meteorological and oceanographical measurements (see below)

User-specified settings (including IOP and solar irradiance file names) are indicated in the input file. All of these must be filled in as specified below and in the template supplied with this code. Fields are described below. DO NOT remove colons or alter text to the left of colons when filling out this file. Also do not indicate units of measurement, only the numerical values.

Station Name: OCEANIA18
acs file*: name and pathway of processed absorption/attenuation file (single spectra)
hs6 file*: name and pathway of particulate backscattering file (single spectra)
acs pathway**:  pathway for hydrolight-compatible absorption/attenuation files. Files must be placed in this location prior to initiating Hydrolight. Hydrolight also will search this pathway "Solar Irradiance file".
hs6 pathway**:  pathway for hydrolight-compatible absorption/attenuation files. Files must be placed in this location prior to initiating Hydrolight
Solar Irradiance file: ascii (.txt) file containing field-sampled above-water solar irradiance. This is usually measured with a refernce sensor
Chl Conc (mg/L): Numerical Chlorophyll concentration
Wavelengths***: Output wavelengths. These can be listed as a matlab style array (e.g. 400:50:700) or as a comma-separated list.
Date (mm-dd-yyyy): Date of field sampling. 
GMT (HH:MM:SS): Greenwhich mean time of field sampling
Water Temperature (deg. C): Numerical water temperature
Salinity (PSU): Salinity
Latitude****: Latitude in decimal form (south is negative)
Longitude****: Longitude in decimal form (west is negative)
Pressure (inHg): Numerical pressue in INCHES of murcury
Humidity (%): Humidity as a percent
Precipitable Water Content (cm): Numerical value expressed in centimeters
Horizontal Visibility (km): Numerical value expressed in kilometers
c-interpolation: ac-s absorption and attenuation channels are slightly offset from each other (typicaly < 1 nm). acsPROCESS_INTERACTIVE. and acsPROCESS_SEABASS.m allow user to interpolate attenuation to absorption-centered wavelengths using "spline". If user performed this interpolation enter "yes". If user opted out enter "no".
Doxaran-Correction: hs6PROCESS_INTERACTIVE. and hs6PROCESS_SEABASS.m allow user to sigma-correct hs6 according to methods described in Doxaran et al. (2016). If user performed this correction enter "yes". If user opted out of this correction enter "no"
Wind Speed (m/s): Numerical value in meters per second.
Depth Bin Size (m): Enter numerical depth bin in meters. This value need not be an integer.
Max Depth (m): Enter numerical maximum depth in meters. This value need not be an integer, but should be divisible by Depth Bin Size.
Bootstrap Iterations: Enter the number of bootstrap iterations. This value MUST be an integer.
