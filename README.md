# Ephemerides and Sight Reduction for the HP Prime Calculator
This repository contains a set of programs written in Prime Programming Language (PPL) for the [HP Prime calculator](https://www.hpcc.org/calculators/hpprime.html) to turn it into a reliable, low-cost celestial navigation computer that can live in a chart table and requires no updates until 2200. It can also be used on any PC or Mac running the [*HP Prime Virtual Calculator*](https://updates.moravia-consulting.com/) program.

The following functionality is provided:
* Astronomical calculations of the ephemerides of the usual celestial navigation bodies (Sun, Moon, Mars, Venus, Jupiter, Saturn, and 58 stars)
* Observation planning by listing the azimuth and elevation of all the visible bodies that meet minimum elevation and azimuth restrictions at a given location at a specified future date and time
* Sight reduction of sextant observations of any of those celestial bodies to Lines of Position (LOPs)
* Plotting of LOPs on a Cartesian plot from which a fix can easily be deduced.
* Determination of the index correction of a sextant from two simple observations of the Sun
* Support for running fixes by translating lines of position by a certain distance on a given bearing

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

![HP Prime 48 G2 calculator](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/hp48g2.png)

The astronomical calculations are derived from the incredible work of Henning Umland which he has been kind enough to share [on his web site](https://celnav.de/). The ephemerides are generally accurate to 0.1' (see **Future Improvements** section).

The sight reduction formulas used in this program were derived from many sources that are usually provided in the comments within the source code.

For an excellent textbook on celestial navigation and the process of sight reduction, refer to [*Celestial Navigation: A Complete Home Study Course*](https://starpath.com/catalog/books/1887.htm) by David Burch and Tobias Burch. The calculations in this program follow the sight reduction process described in the book.

# Installing the Program
The program can be installed on an HP Prime calculator or on a PC or Mac running the [HP Prime Virtual Calculator](https://www.hpcalc.org/details/8939) from the source files in the */src* folder of this repository or from the binary files in the */bin* folder.

## Prerequisites

In order to use and install this program, you need to download this repository to your computer and you need to have the [*HP Connectivity Kit*](https://updates.moravia-consulting.com/) running on your computer and working with either an HP Prime calculator connected to your computer with a USB cable or with the [*HP Prime Virtual Calculator*](https://www.hpcalc.org/details/8939) program running on the same computer as the HP Connectivity Kit.

### Downloading this Repository

You can download a ZIP archive containing all the files in this repository from [this link](https://github.com/placidanomaly/HPPrimeSightReduction/archive/refs/heads/main.zip). Extract it to some folder on your computer. Alternatively, if you are familiar with *git*, you can clone the repository into your current folder in a command shell window with `git clone https://github.com/placidanomaly/HPPrimeSightReduction.git`.

### *HP Connectivity Kit* and *HP Prime Virtual Calculator*

Follow these steps to download and install the HP Connectivity Kit and the HP Prime Virtual Calculator program:

1. Download and install the *HP Connectivity Kit* program from this [link](https://updates.moravia-consulting.com/)
2. If desired, download and install the *HP Prime Virtual Calculator* program from this [link](https://updates.moravia-consulting.com/)
3. Launch the *HP Connectivity Kit* program
4. Connect an HP Prime Calculator to the computer with a USB cable, or launch the *HP Prime Virtual Calculator* program, and confirm that the calculator appears in the **Calculators** window of the Connectivity Kit
5. Ensure that the **Content** window is visible in the *HP Connectivity Kit* program. To make it appear, select the **Window->Content** menu option


## Installing from Binaries (RECOMMENDED)

To install from the binaries, the *.hpprgm* files must be loaded into the Connectivity kit:

1. Drag all the *.hpprgm* files in the */bin* folder of the repository into the **Content** section of the *HP Connectivity Kit* program
2. Drag all the files in the **Content** window of the *HP Connectivity Kit* program onto the calculator icon in the **Calculators** window

## Installing from Source Files

1. Expand the calculator and the **Programs** section of the calculator in the *HP Connectivity Kit* program
5. Right-click on **Program** and select **New**
6. Enter the name *Earth* and press Enter. An empty editor window will open
7. Open the **earth.txt** file from this repository in a text editor on your computer
8. Select all the text (Ctrl-A), copy it to the clipboard (Ctrl-C), and paste it into the editor window in the *HP Connectivity Kit* program (Ctrl-V)
9. Save the file (Ctrl-S) and close the editor window
10. Repeat steps 5-8 above for each text file in the repository
11. On the calculator, go to the **Programs** page with <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="1" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/1.png" valign="middle"> and confirm that all the programs are loaded
12. Open each program and hit <img alt="Check" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/check.png" valign="middle"> to confirm that there are no syntax errors

## Confirming that Everything Works
When all is done, your Connectivity Kit screen should look like this:

![Connectivity Kit screen shot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/connectivity.png)

To confirm that the installation was successful, perform the following verification:

1. On the calculator, open the Programs page using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="1" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/1.png" valign="middle"> keys. Select the **Sight Reduction** program using the arrows, press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key, select **RESET_SIGHTS** using the arrows and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. This will initialize all the necessary variables for the program to work.
2. Select the **Sight Reduction** program, press <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle">, select **EPHEMERIDES** using the arrows and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. Fill out the form with a date, time, and location following the conventions in the next section and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. If everything was installed properly, the requested ephemerides will be displayed and you can scroll through them using the touchscreen. Check the values against an Almanac for accuracy. If this fails, double-check that all the programs are installed and, if you installed them from source, that the programs were checked per step 12 above.

# Using the Program

All the functionality is accessed through the **Sight Reduction** program. The other programs support astronomical calculations that are too voluminous to fit within a single program. Those programs need to be present for **Sight Reduction** to work, but they should not be invoked by the user under normal usage scenarios.

## Units and Conventions
The program relies on dates, times, positions, and other information to perform the calculations. Whenever a field is highlighted for input, the line at the bottom of the screen will provide hints as to which unit and format should be used for that field. Keep in mind that the units are not consistent, they follow the conventions of celestial navigation. For example positions, hour angles, and declinations are expressed in degrees, corrections are in arc minutes, and the semi-diameter of celestial bodies is expressed in arc seconds, so pay attention to the input hints.

### Negative Numbers

Negative numbers must be prefixed by a `-` symbol entered using the <img alt="+/-" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/plusminus.png" valign="middle"> key, and NOT with the subtraction key, which will cause an error. If the calculator is in Reverse Polish Notation (RPN) mode, all characters in an input field must be cleared before a negative value can be entered. This is why we recommend setting the calculator in Textbook mode (the default value) using the **SHIFT-Home** key combination prior to using this program. An alternative to avoid having to enter negative numbers is to enter western longitudes as their corresponding eastern equivalent, e.g. instead of entering 45W, which must be entered as `-45` as will be explained later, you can enter 315E, which is entered as `315`.

### Position Format

Positions are represented in degrees of latitude and longitude which can be entered either as *DD°MM'SS"* using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="abc" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/abc.png" valign="middle"> key combination or in decimal degrees *DD.ddddddd*. Northern latitudes are positive, so 14°45'21"N is entered as `14°45'21"`, while southern latitudes are negative, so 20.2321S is entered as `-20.2321`. Same with declination: N45.2345 is represented as `45.2345` while S12°51'03" is represented as `-12°51'03"`. Positive values of longitude greater than 180° will be converted to a negative value corresponding to the western longitude, e.g. 220 will be converted to -140.

Celestial navigation positions, declinations, corrections, hour angles, etc., are traditionally represented using degrees and decimal minutes to one decimal place, e.g. *DD°MM.m'*, but the calculator does not natively support that format. Decimal minutes must be converted to arc seconds which are equal to the decimal part of minutes multiplied by 6. For example, S24°8.4' must be entered as `-24°8'24"`. That being said, the program usually outputs values using decimal minutes.

### Date Format

Date values are represented using the native calculator format which is *YYYY.MMDD*. For example, April 23, 2026 must be entered as `2026.0423`.

### Time Format

Time values are represented in 24-hour hours using the same format as position degrees, i.e. *HH°MM'SS"*, using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="abc" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/abc.png" valign="middle"> keys. For example 11:43:12pm is entered as `23°43'12"`.

## Initialization \*IMPORTANT\*
The first thing to do is to initialize lists and variables, set default values, and set the time and timezone of the calculator. This must also be done every time after editing a program even if no changes were made to it. Proceed as follows:

1. Highlight the **Sight Reduction** program and press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key
2. From the list of options, pick **RESET_SIGHTS** on the touchscreen or with the arrows and the <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> key, or press the <img alt="8" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/8.png" valign="middle"> key. Click any key to dismiss the confirmation message.

![Resetting variables](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

4. Now re-run the program and pick **SET_TIME** and set the calculator's local time clock and timezone:

   * **Local time**: the local time to which to set the calculator. Enter a time a few seconds in the future and click the <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> soft key when your watch reads the time entered
   * **UTC Offset**: the number of hours ahead of or behind UTC. Use a positive value for locations West of Greenwhich and negative for East (e.g. -5 for New York standard time). Keep in mind that this offset changes with Daylight Savings Time (DST)

![Setting the time and timezone](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/settime.png)

## Planning Observations
It can be helpful to know which celestial bodies will be visible and where ahead of an observation session with the sextant so that the bodies to be observed can be selected ahead of time. This is done with the **LIST_VISIBLE_BODIES** function of the **Sight Reduction** program. You will be prompted to enter the parameters for listing the bodies:

   * **Date**: the date on which the observations will be made in YYYY.MMDD format
   * **Time**: the approximate UTC time at which the observations will be made in HH°MM'SS" format
   * **Latitude**: the assumed latitude in degrees from which the observations will be made
   * **Longitude**: the assumed longitude in degrees from which the observations will be made
   * **Elevation**: the minimum elevation in degrees of the celestial bodies to be included in the list
   * **Azimuth from**: the true heading in degrees of the beginning of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list
   * **Clockwise to**: the true heading in degrees of the end of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list

![Parameters for listing bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_input.png)

The output will be shown in the Spreadsheet app and will include, for each celestial body meeting the minimum elevation and azimuth range criteria, the azimuth, elevation, Greenwhich Hour Angle (GHA), declination (dec), and the semi-diameter in arc seconds of the body (if applicable):

![List of bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_output.png)

## Calculating Index Correction from Sun diameter (OPTIONAL)

The program contains a function to apply the index correction method described in [this document](https://www.starpath.com/online/celestial/solar_ic.pdf). After running this program, the default value for the index correction in the sight reduction forms will be set to the value calculated by this procedure (otherwise the default index correction value will be zero). To run the program, highlight the **Sight Reduction** program and hit the <img alt="6" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/6.png" valign="middle"> key to run the **SOLAR_IC** program. The program briefly describes the measurements that need to be taken:

![Solar IC intro](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_intro.png)

Values for the *Below* and *Above* observations as read on the sextant, in arc minutes, can be entered in the input form. Do NOT correct the off scale *Below* reading by subtracting it from 60, the program will do that for you. Use the value directly read on the instrument.

![Solar IC input](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_input.png)

The program will display the calculated index correction result as well as the implied semi-diameter of the sun, which is then compared with the actual semi-diameter of the sun at the current time. This allows validating the inputs used before applying the calculated index correction to future sights.

![Solar IC output](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_output.png)

After pressing a key, the program prompts whether to accept or reject the calculated index correction. If accepted, the value will be applied to all sights that did not have a manually entered index correction and will be used as the default value for new sights.

## Reducing Sights
Performing a sight reduction is a straightforward process: 

1. To run the program, highlight the **Sight Reduction** program and press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key.

1. Reset all previous observations and calculations by running **RESET_SIGHTS** in the **Sight Reduction** program.

![Sight Reduction programs](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

3. Enter a new observation: select **SIGHT** and press the <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> soft key.

4. The program can store up to 10 different observations, each resulting in a line of position, and they are accessed by an LOP register number from 1 to 10. Select an LOP register for this observation, let's say **1** for this first one, and hit the <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> soft key.

![Observation register selection](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input1.png)

6. On the 2nd screen:
   * **Body**: select the body that was observed, let's say the **Sun** for this one
   * **Date**: the date of the observation in HP Prime date format (*YYYY.MMDD*) (for ephemeris calculations)
   * **Time UTC**: enter the UTC time of the observation in the calculator time format (*HH°MM'SS"*)(for ephemeris and local hour angle (LHA) calculations)   
   * **HS**: enter the observed height from the sextant in degrees, arc minutes and arc seconds format (DD°MM'SS"). Sextants show fractional minutes in decimals which can be converted to arc seconds by simply multiplying the decimal part of the minutes by 6, e.g. 13°32.4' on the sextant must be entered as 13°32'24".
   * **Artificial**: check this box if the observation was made on an artificial horizon. If that's the case, the value entered in HS must be the actual sextant reading, i.e. double the actual body height. When this box is checked, the index correction will be applied before dividing the reading by half and no dip correction will be applied

![Basic observation data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input2.png)

7. On the 3rd screen, enter the observation conditions which will result in altitude corrections:
   * **IC**: the index correction of the sextant in arc minutes, negative values for "on-scale" correction and positive for "off-scale"
   * **HE**: eye height from the horizon in feet (for dip correction)
   * **Dip short**: distance in nautical miles (nm) from observer where the horizon ends (e.g. the other side of a large lake), or zero if an infinite horizon is used as reference for the observation
   * **Temp**: the air temperature in degrees C (for refraction correction)
   * **Pressure**: the atmospheric pressure at sea level in millibars (for refraction correction)

![Observation correction data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input3.png)

8. On the 3rd screen, enter body-specific data and the assumed position
   * **Limb**: for the sun, whether the observation was made on the lower or upper limb (for semi-diameter correction). Other bodies will have body-specific parameters to enter here: the observed limb for a moon sight and the star name for a star sight
   * **DR Lat**: the latitude of the assumed or DR position in degrees at the time of the observation
   * **DR Lon**: the longitude of the assumed or DR position in degrees at the time of the observation

![More input data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input4.png)

9. The calculator will display the values for observed height *Ho*, Greenwhich Hour Angle *GHA*, declination *dec*, Local Hour Angle *LHA*, and the calculated height *Hc* of the body. Click **OK**

![Calculation results](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output1.png)

11. The calculator will then display the usual 4 parameters of the line of position: LOP register, distance *a* from the LOP either *TOWARD* or *AWAY* from the body, azimuth *Zn* to the body, and the assumed position latitude and longitude as entered (no correction of assumed position is necessary here because fractional LHA and Zn can easily be handled by the calculator). These parameters enable plotting of the line of position.

![LOP parameters](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output2.png)

12. Lastly, the calculator displays the equation for the line of position in a longitude (x) and latitude (y) Cartesian plane which can be used to plot it in a program. That equation is stored in the `F` register of the Function app of the calculator corresponding to the LOP register selected, e.g. LOP 1 will be stored in `F1`, which means they can be plotted using the calculator's Function app.

![LOP Equation](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output3.png)

## Making a Fix

Once you've entered 2 or more sights in different LOP registers, you can make a fix from a graphical representation of the LOPs on a Cartesian plane. To do that, run the **Sight Reduction** program and select **PLOT LOPs**. This will open the calculator's Function app and a line of position will be plotted for each LOP defined in the **SIGHT** program. The calculator functions can then be used to calculate the intersection of LOPs, etc., and the cursor can be used to manually find the centroid or some other position in the "cocked hat" to make a fix. In order to determine which line color corresponds to which LOP, use the **Symb** key to view the color coding and the corresponding LOP equations, and use the **Plot** key to go back to the graph.

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

# Future Improvements
The ephemeris calculations are usually accurate to within less than 0.1' of the values in the Almanac for the period 1900-2200 (subject to Delta T adjustments), but errors of up to 0.3' are sometimes seen. This is sufficient for most practical cases of celestial navigation but perfect precision would be better. The differences are still being investigated because the same program in Javascript from Henning Umland's web site seems to always output the exact same numbers as the Almanac. The possibility of a discrepancy in the code is one theory but a more likely one is that the lower number of significant digits in the calculator vs. a regular computer introduces rounding errors that add up in the lengthy calculations, but that has yet to be proven.

# Contact
This program was developed by [Charles Vaillancourt](mailto:charles.vaillancourt@gmail.com). I welcome comments and suggestions for improvement and will gladly review pull requests for inclusion in the program.
