# Ephemeris and Sight Reduction for the HP Prime Calculator
This repository contains a set of programs written in Prime Programming Language (PPL) for the [HP Prime 48 calculator](https://www.hpcc.org/calculators/hpprime.html) to perform astronomical calculations for the ephemerides of the usual bodys used in celestial navigation (Sun, Moon, Mars, Venus, Jupiter, Saturn, and 58 stars), and the sight reduction of sextant observations to Lines of Position (LOPs) which rely on those ephemerides. The LOPs are represented in a Cartesian plot from which a fix can readily be deduced. The program also provides support for running fixes through a function that allows the translation of lines of position by a certain distance on a given bearing.

Of course there are other more accurate methods to derive a fix from sextant observations without even an assumed position but which rely on numerical methods that can't be performed without a more powerful computer. This program merely automates the manual process but it results in a perfectly usable, reliable, low-cost sight reduction calculator that can live in the chart table and requires no updates until 2100.

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

![HP Prime 48 G2 calculator](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/hp48g2.png)

The astronomical calculations are derived from the incredible work of Henning Umland which he has been kind enough to share [on his web site](https://celnav.de/).

The sight reduction formulas used in this program were derived from many sources that are usually listed in the source code comments.

For an excellent textbook on celestial navigation and the process of sight reduction, refer to *Celestial Navigation: A Complete Home Study Course* by David Burch and Tobias Burch.

# Installing the Program
The program can be installed on the calculator or on the [virtual calculator program](https://www.hpcalc.org/details/8939) from the *.txt* source files in the main directory of this repository or from the binaries in the */bin* directory. 
When all is done, your Connectivity Kit screen should look like this:

![Connectivity Kit screen shot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/connectivity.png)

## Installing from the Source Files

1. Download and install the [HP Connectivity Kit](https://updates.moravia-consulting.com/)
2. Launch the HP Connectivity Kit program
3. Connect an HP Prime Calculator to the computer with a USB cable and confirm that the Connectivity Kit sees the calculator
4. Expand the Program section of the calculator
5. Right-click on **Program** and select **New**
6. Enter the name "Earth" and press Enter. An empty editor window will open
7. Open the **earth.txt** file from this repository in a text editor
8. Select all the text (Ctrl-A), copy it to the clipboard (Ctrl-C), and paste it into the editor window in the HP Connectivity Kit program (Ctrl-V)
9. Save the file (Ctrl-S) and close the editor window
10. Repeat steps 5-8 above for each text file in the repository
11. On the calculator, go to the **Programs** page (Shift-1) and confirm that all the programs are loaded
12. Open each program and hit **Check** to confirm that there are no syntax errors
13. Select the **Sight Reduction** program, press **Run**, select **RESET_SIGHTS** and press **Enter**. This will initialize all the necessary variables for the program to work.
14. To confirm everything is working, select the **Sight Reduction** program, press **Run**, select **EPHEMERIDES** and press **Enter**. Fill out the form and press **Enter**. The requested ephemerides should be displayed on the screen. Check them against an Almanac.

## Installing from the Binaries

To install from the binaries, the *.hpprgm* files must be loaded into the Connectivity kit:

1. Download and install the [HP Connectivity Kit](https://updates.moravia-consulting.com/)
2. Launch the HP Connectivity Kit program
3. Connect an HP Prime Calculator to the computer with a USB cable and confirm that the Connectivity Kit sees the calculator
4. Drag all the *.hpprgm* files in the */bin* directory of the repository into the **Content** section of the HP Connectivity Kit program
5. Drag all the files in the **Content** window of the HP Connectivity Kit program onto the **Programs** section label of the calculator

After this setup, all the functions can be accessed by running the **Sight Reduction** program.

# Using the Program
## Initialization and Setting the Time and Timezone
The first thing to do is to initialize lists and variables, set default values, and set the time and timezone of the calculator:

1. Highlight the **Sight Reduction** program and press the **Run** soft key
2. From the list of options, pick **RESET** on the touchscreen or with the arrows and the *Enter* key. Click any key to dismiss the confirmation message.
3. Now re-run the program and pick **SET_TIME** and set the calculator's local time clock and the timezone:

   * **Local time**: the local time to which to set the calculator. Enter a time a few seconds in the future and click the **Ok** soft key when your watch reads the time entered
   * **UTC Offset**: the number of hours ahead or behind of UTC. Use a positive value for locations West of Greenwhich and negative for East. Keep in mind that this offset changes with Daylight Savings Time (DST)   

![Setting the time and timezone](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/settime.png)

## Planning Observations
It can be helpful to know which celestial bodies will be visible and where ahead of an observation session with the sextant so that the bodies to be observed can be selected ahead of time. This is done with the **LIST_VISIBLE_BODIES** function of the **Sight Reduction** program. You will be prompted to enter the parameters for listing the bodies:

   * **Date**: the date on which the observations will be made in YYYY.MMDD format
   * **Time**: the approximate UTC time at which the observations will be made in HH°MM'SS" format using the Shift-(a b/c) key
   * **Latitude**: the assumed latitude from which the observations will be made in either DD°MM'SS" format using the Shift-(a b/c) key or in decimal degrees DD.ddddddd...
   * **Longitude**: the assumed longitude from which the observations will be made in degrees
   * **Elevation**: the minimum elevation of the celestial bodies to included in the list in degrees
   * **Azimuth from**: the true heading in degrees of the beginning of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list
   * **Clockwise to**: the true heading in degrees of the end of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list

![Parameters for listing bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_input.png)

The output will be shown in the Spreadsheet app and will include, for each celestial body meeting the minimum elevation and azimuth range criteria, the azimuth, elevation, Greenwhich Hour Angle (GHA), declination (dec), and the semi-diameter in seconds of the body (if applicable):

![List of bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_output.png)

## Performing a Sight Reduction
All the steps to perform a sight reduction, from capturing sextant observations to plotting lines of position and identifying a fix are done within the **Sight Reduction** program. The other programs support ephemeris calculations which were too big to fit within a single program. Those programs need to be present for **Sight Reduction** to work, but they do not need to be invoked by the user under normal usage scenarios. 

1. To run the program, highlight the **Sight Reduction** program and press the **Run** soft key.

1. Reset all previous observations and calculations by running **RESET_SIGHTS** in the **Sight Reduction** program.

![Sight Reduction programs](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

3. Enter a new observation: select **SIGHT** and press the **Enter** soft key.

4. The program can store up to 10 different observations, each resulting in a line of position, and they are accessed by an LOP register number from 1 to 10. Select an LOP register for this observation, let's say **1** for this first one, and hit the **OK** soft key.

![Observation register selection](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input1.png)

6. On the 2nd screen:
   * **Body**: select the body that was observed, let's say the **Sun** for this one
   * **Date**: the date of the observation in HP Prime date format (YYYY.MMDD) (for ephemeris calculations)
   * **Time UTC**: enter the UTC time of the observation in the calculator time format (HH°MM'SS") using the Shift-(a b/c) key combination (for ephemeris and local hour angle (LHA) calculations)   
   * **HS**: enter the observed height from the sextant in degrees, arc minutes and arc seconds format (DD°MM'SS") using the Shift-(a b/c) key. Sextants show fractional minutes in decimals which can be converted to arc seconds by simply multiplying the decimal part of the minutes by 6, e.g. 13°32.4' on the sextant must be entered as 13°32'24".

![Basic observation data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input2.png)

7. On the 3rd screen, enter the observation conditions which will result in altitude corrections:
   * **IC**: the index correction of the sextant in minutes, negative values for "on-scale" correction and positive for "off-scale"
   * **HE**: eye height from the horizon in feet (for dip correction)
   * **Dip short**: distance in nautical miles (nm) from observer where the horizon ends (e.g. the other side of a large lake), or zero if an infinite horizon is used as reference for the observation
   * **Temp**: the air temperature in degrees C (for refraction correction)
   * **Pressure**: the atmospheric pressure at sea level in millibars (for refraction correction)

![Observation correction data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input3.png)

8. On the 3rd screen, enter body-specific data and the assumed position
   * **Limb**: for the sun, whether the observation was made on the lower or upper limb (for semi-diameter correction). Other bodies will have body-specific parameters to enter here: the observed limb for a moon sight and the star name for a star sight
   * **DR Lat**: the latitude of the assumed or DR position at the time of the observation in DMS format (DD°MM'SS")
   * **DR Lon**: the longitude of the assumed or DR position at the time of the observation in DMS format (DD°MM'SS")

![More input data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input4.png)

9. The calculator will display the values for observed height *Ho*, Greenwhich Hour Angle *GHA* of the body, declination *dec* of the body, Local Hour Angle *LHA* of the body, and the calculated height *Hc* of the body. Click **OK**

![Calculation results](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output1.png)

11. The calculator will then display the usual 4 parameters of the line of position: LOP register, distance *a* from LOP either *TOWARD* or *AWAY* from the body, azimuth *Zn* to the body, and the assumed position latitude and longitude. These parameters enable plotting of the line of position.

![LOP parameters](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output2.png)

12. Lastly, the calculator displays the equation for the line of position in a longitude (x) and latitude (y) cartesian plane which can be used to plot it in a program. That equation is stored in the F register of the Function app of the calculator corresponding to the LOP register selected, e.g. LOP 1 will be stored in F1, which means they can be plotted using the calculator's Function app.

![LOP Equation](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output3.png)

14. Once you've entered 2 or more sights in different LOP registers, you can view the LOPs on a graph: run the **Sight Reduction** program and select **PLOT LOPs**. This will open the calculator's Function app and a line of position will be plotted for each LOP defined in the **SIGHT** program. The calculator functions can then be used to calculate the intersection of LOPs, etc., and the cursor can be used to manually find the centroid or some other position in the "cocked hat" to make a fix.

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

# Remaining Work
The ephemeris calculations are usually accurate to within less than 0.1' of the values in the Almanac for the period 1900-2100, but errors up to 0.3' are sometimes seen. This is probably sufficiently accurate for most practical cases of celestial navigation but perfect precision would be better. The differences are still being investigated because the same program in Javascript from Umland's web site produces the exact same numbers as the Almanac. The possibility of a discrepancy in the code is one theory. Another is that it would be due to the lower number of significant digits in the calculator vs. a regular computer, but that has yet to be proven.

# Contact
This program was developed by [Charles Vaillancourt](mailto:charles.vaillancourt@gmail.com).
