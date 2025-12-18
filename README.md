# Ephemeris and Sight Reduction for the HP Prime Calculator
This repository contains a set of programs to perform astronomical calculations of the ephemerides of the usual bodys used in celestial naviation, and the sight reduction of sextant observations to Lines of Position (LOPs) which relies on those ephemerides. The LOPs are represented in a graph from which a fix can readily be deduced. The program also provides support for running fixes through a function that allows the translation of lines of position by a certain distance on a given bearing.

![LOP plot example](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

The astronomical calculatons are derived from the incredible work of Henning Umland which he has been kind enough to share [on his web site](https://celnav.de/).

The sight reduction formulas used in this program were derived from many sources that are usually listed in the source code comments.

For an excellent textbook on celestial navigation and the process of sight reduction, refer to * *Celestial Navigation: A Complete Home Study Course* * by David Burch and Tobias Burch.

# Installing the Program
The program can be installed on an HP Prime Calculator using a USB connection to a computer or in the HP Prime Virtual Calculator program. This is the procedure to install it on a calculator:

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

When all is done, your Connectivity Kit screen should look like this:
![Connectivity Kit screen shot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/connectivity.png)

After this setup, sight reduction can be preformed by choosing the **SIGHT** option of the **Sight Reduction** program.

# Performing a Sight Reduction
All the steps to perform a sight reduction, from capturing sextant observations to plotting lines of position and identifying a fix are done within the **Sight Reduction** program. The other programs support ephemeris calculations which were too big to fit within a single program. Those programs need to be present for **Sight Reduction** to work, but they do not need to be invoked by the user under normal usage scenarios. 

1. To run the program, highlight the **Sight Reduction** program and press the **Run** soft key.

1. Reset all previous calculations by running **RESET_SIGHTS** in the **Sight Reduction** program.

![Sight Reduction programs](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

3. Enter a new observation: select **SIGHT** and press the **Enter** soft key.

4. Select an observation register for this observation, let's say **1** for this first one, and hit the **OK** soft key. (The program can store up to 10 different observations, each resulting in a line of sight, and they are accessed by that number.)

![Observation register selection](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input1.png)

6. On the 2nd screen:
   * **Body**: select the body that was observed, let's say the **Sun** for this one
   * **Date**: the date of the observation in HP Prime date format (YYYY.MMDD) (for ephemeris calculations)
   * **UTC**: enter the UTC time of the observation in the calculator time format (HH°MM'SS") using the Shift-(a b/c) key combination (for ephemeris and local hour angle (LHA) calculations)   
   * **HS**: enter the observed height from the sextant in degrees, arc minutes and arc seconds format (DD°MM'SS") using the Shift-(a b/c) key. Sextants show fractional minutes in decimals which can be converted to seconds by simply multiplying the decimal part of the minutes by 6, e.g. 13°32.4' on the sextant must be entered as 13°32'24".

![Basic observation data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input2.png)

7. On the 3rd screen, enter the observation conditions:
   * **IC**: the index correction in minutes, negative for "on-scale" correction adn positive for "off-scale"
   * **HE**: eye height from the horizon in feet (for dip correction)
   * **Dip short**: distance in nautical miles (nm) from observer where the horizon stops (e.g. the other side of a large lake), or zero if a true horizon is used as reference for the observation
   * **Temp**: the air temperature in degrees C (for refraction correction)
   * **Pressure**: the atmospheric pressure at sea level in millibars (for refraction correction)

![Observation correction data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input3.png)

8. On the 3rd screen, enter body-specific data and the assumed position
   * **Limb**: for the sun, whether the observation was made on the lower or upper limb -- other bodies will have body-specific parameters to enter here (for semi-diameter correction)
   * **DR Lat**: the latitude of the assumed or DR position at the time of the observation in DMS format (DD°MM'SS")
   * **DR Lon**: the longitude of the assumed or DR position at the time of the observation in DMS format (DD°MM'SS")

![More input data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input4.png)

9. The calculator will present the values for Ho (observed height), GHA (Greenwhich Hour Angle) of the body, dec (declination) of the body, LHA (Local Hour Angle) of the body, and Hc (calculated height) of the body. Click **OK**

![Calculation results](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output1.png)

11. The calculator will then present the parameters of the line of position: LOP register, a (distance from LOP) either TOWARD or AWAY from the body, Zn (azimuth) to the body, and the assumed position latitude and longitude. These parameters enable plotting of the line of position.

![LOP parameters](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output2.png)

12. Lastly, the calculator presents the equation for the line of position which can be used to plot it in a program. That equation is stored in the F register of the Function app of the calculator corresponding to the LOP register selected, e.g. LOP 1 will be stored in F1.

![LOP Equation](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output3.png)

14. Once you've entered 2 or more sights in different LOP registers, you can view the LOPs on a graph: run the **Sight Reduction** program and select PLOT LOPs. A line of position will be plotted for each LOP defined in the **SIGHT** program. The calculator functions can then be used to calculate the intersection of LOPs, etc., and the cursor can be used to find the centroid of the "cocked hat" to make a fix.

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

# Remaining Work
The ephemeris calculations are usually accurate to within less than 1' of the values in the Almanac for the period 1900-2100, but errors up to 2' are sometimes seen. This is probably sufficiently accurate for most practical cases of celestial navigation but perfect precision would be better. The differences are still being investigated because the same program in Javascript from Umland's web site produces the exact same numbers as the Almanac. The possibility of a discrepancy in the code is one theory. Another is that it would be due to the lower number of significant digits in the calculator vs. a regular computer, but that has yet to be proven.

# Contact
This program was developed by [Charles Vaillancourt](mailto:charles.vaillancourt@gmail.com).
