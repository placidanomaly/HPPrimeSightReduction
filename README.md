# Ephemerides and Sight Reduction for the HP Prime Calculator
This repository contains a set of programs written in Prime Programming Language (PPL) for the [HP Prime calculator](https://www.hpcc.org/calculators/hpprime.html) to turn it into a reliable, low-cost celestial navigation computer that can live in a chart table and requires no updates until the year 2200. It can also be used on any PC or Mac running the [*HP Prime Virtual Calculator*](https://updates.moravia-consulting.com/) program.

The following functionality is provided:
* Astronomical
  * Ephemerides of the Sun, Moon, Mars, Venus, Jupiter, Saturn, and the usual 58 stars used in celestial navication
  * Delta T, equation of time, obliquity of the ecliptic, etc.
  * Rise and set times of the Sun and all other celestial bodies, civil and nautical twilight times
  * Semi-diameter of the planets and the Moon
  * Moon phase
  * Centroid corrections for the partial illumination of Venus and Mars
  * Interactive stereographic projection of the sky (aka star finder plot) at a given location and time

* Navigation
  * Observation planning by listing all observable bodies (i.e. meeting user-specified altitude and azimuth constraints) during morning and evening nautical twilight and at any time of the day with their respective GHA, declination, azimuth, true altitude, apparent altitude, and semi-diameter
  * Sight reduction of sextant observations of any of those celestial bodies to Lines of Position (LOPs)
  * Running fix calculations through translation of lines of position by a certain distance on a given bearing
  * Plotting of LOPs on a Cartesian plot from which a fix can easily be deduced
  * Determination of the index correction of a sextant from two simple observations of the Sun

<img alt="Sample LOP plot" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png" valign="top">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img alt="Sample LOP plot" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/starfinder.png" valign="top">

![HP Prime 48 G2 calculator](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/hp48g2.png)

The astronomical calculations are derived from [the incredible work of Henning Umland](https://celnav.de/). The ephemerides are generally accurate to 0.1' from the 19th to 22nd centuries inclusively (1800-2200) (see **Future Improvements** section).

The sight reduction formulas used in this program were derived from many sources that are usually provided in the comments within the source code.

For an excellent textbook on celestial navigation and the process of sight reduction, refer to [*Celestial Navigation: A Complete Home Study Course*](https://starpath.com/catalog/books/1887.htm) by David Burch and Tobias Burch. The calculations in this program follow the sight reduction process described in the book.

# Table of Contents
* [**Installing the Program**](#installing_the_program)
  * [Prerequisites](prerequisites)
    * [Downloading this repository](downloading-this-repository)
    * [*HP Connectivity Kit* and *HP Prime Virtual Calculator*](#hp-connectivity-kit-and-hp-prime-virtual-calculator)
  * [Installing from Binaries](#installing-from-binaries-recommended)
  * [Installing from Source Files](#installing-from-source-files)
  * [Confirming that Everything Works](#confirming-that-everything-works)
    
* [**Using the Program**](#using-the-program)
  * [Units and Conventions](#units-and-conventions)
    * [Negative Numbers](#negative-numbers)
    * [Position and Angle Format](#position-and-angle-format)
    * [Date Format](#date-format)
    * [Time Format](#time-format)
    * [Dark Mode](#dark-mode)
  * [Initialization](#initialization)
  * [Planning Observations](#planning-observations)
  * [Reducing Sights](#reducing-sights)
  * [Running Fixes](#running-fixes)
  * [Making a Fix](#making-a-fix)
    * [Manual Fix](#manual-fix)
    * [Computed Fix](#computed-fix)
  * [Ephemerides](#ephemerides)
  * [Star Finder](#star-finder)
  * [Setting Default Index Correction](#setting-default-index-correction)
    * [Direct Entry](#direct-entry)
	* [Calculation from Sun diameter measurement](#calculation-from-sun-diameter-measurement)

# Installing the Program
The program can be installed on an HP Prime calculator or on a PC or Mac running the [HP Prime Virtual Calculator](https://www.hpcalc.org/details/8939) from the source files in the */src* folder of this repository or from the binary files in the */bin* folder.

## Prerequisites

In order to use and install this program, you need to download this repository to your computer and you need to have the [*HP Connectivity Kit*](https://updates.moravia-consulting.com/) running on your computer and working with either an HP Prime calculator connected to your computer with a USB cable or with the [*HP Prime Virtual Calculator*](https://www.hpcalc.org/details/8939) program running on the same computer as the HP Connectivity Kit.

### Downloading this Repository

You can download a ZIP archive containing all the files in this repository from [this link](https://github.com/placidanomaly/HPPrimeSightReduction/archive/refs/heads/main.zip). Extract it to some folder on your computer. Alternatively, if you are familiar with *git*, you can clone the repository into your current folder in a command shell window with `git clone https://github.com/placidanomaly/HPPrimeSightReduction.git`.

### *HP Connectivity Kit* and *HP Prime Virtual Calculator*

Follow these steps to download and install the *HP Connectivity Kit* and the *HP Prime Virtual Calculator* programs:

1. Download and install the *HP Connectivity Kit* program from this [link](https://updates.moravia-consulting.com/)
2. If desired, download and install the *HP Prime Virtual Calculator* program from this [link](https://updates.moravia-consulting.com/)
3. Launch the *HP Connectivity Kit* program
4. Connect an HP Prime Calculator to the computer with a USB cable, or launch the *HP Prime Virtual Calculator* program, and confirm that the calculator appears in the **Calculators** window of the Connectivity Kit.
> **NOTE:** endpoint protection software like Windows Defender can interfere with the *HP Connectivity Kit* program. Try disabling any such software if you're having trouble connecting to the *HP Prime Virtual Calculator*.

## Installing from Binaries (RECOMMENDED)

To install from the binaries, the *.hpprgm* files must be loaded into the Connectivity kit:

1. Launch the *HP Connectivity Kit* program and ensure the **Content** window is displayed. If not, use the **Window->Content** menu to display it
2. Drag all the *.hpprgm* files in the */bin* folder of the repository into the **Content** window of the *HP Connectivity Kit* program
3. Drag all the files in the **Content** window of the *HP Connectivity Kit* program onto the calculator icon in the **Calculators** window
4. Leave the calculator alone for about 2 minutes while programs are being loaded

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
When all is done, your *HP Connectivity Kit* screen should look like this:

![Connectivity Kit screen shot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/connectivity.png)

To confirm that the installation was successful, perform the following verification:

1. On the calculator, open the Programs page using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="1" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/1.png" valign="middle"> keys. Select the **Sight Reduction** program using the arrows, press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key, select **RESET_SIGHTS** using the arrows and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. This will initialize all the necessary variables for the program to work.
2. Select the **Sight Reduction** program <ins>using the arrows (the big round button) on the calculator</ins> (see note below), press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key on the screen, select **EPHEMERIDES** using the arrows and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. Fill out the form with a date, time, and location following the conventions in the next section and press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle">. If everything was installed properly, the requested ephemerides will be displayed and you can scroll through them using the touchscreen. Check the values against an Almanac for accuracy.
3. If anything fails, double-check that all the programs are installed. Open each one of them using the <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> key. Validate that the file is not empty and push the <img alt="Check" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/check.png" valign="middle"> soft key per Step 12 in the *Installing from Source* section. If the file is empty, try reinstalling the binary file. If that fails, install it from source following the instructions in the previous section. If you're stuck here, contact the author at the address at the bottom of this document.

> **IMPORTANT**: if you inadvertently click on a program name on the touchscreen or press <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> while a program name is highlighted, you will enter the source code view where you can edit the program. Press the **ESC** key to leave the source code view. IF YOU OPEN THE **SIGHT REDUCTION** PROGRAM FOR EDITING, IT WILL CLEAR ALL YOUR SIGHTS. Instead, use the arrows to navigate to a program and click the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key to launch it.

# Using the Program

All the functionality is accessed through the **Sight Reduction** program. The other programs support astronomical calculations that are too voluminous to fit within a single program. Those programs need to be present for **Sight Reduction** to work, but they should not be invoked by the user under normal usage scenarios.

## Units and Conventions

The program relies on dates, times, positions, and other information to perform the calculations. Whenever a field is highlighted for input, the line at the bottom of the screen will provide hints as to which unit and format should be used for that field. Keep in mind that the units are not consistent, they follow the conventions of celestial navigation. For example positions, hour angles, and declinations are expressed in degrees, corrections are in arc minutes, and the semi-diameter of celestial bodies is expressed in arc seconds, so pay attention to the input hints.

### Negative Numbers

Negative numbers must be prefixed by a `-` symbol entered using the <img alt="+/-" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/plusminus.png" valign="middle"> key, and NOT with the subtraction key, which will cause an error. If the calculator is in Reverse Polish Notation (RPN) mode, all characters in an input field must be cleared before a negative value can be entered. This is why we recommend setting the calculator in Textbook mode (the default value) using the **SHIFT-Home** key combination prior to using this program. An alternative to avoid having to enter negative numbers is to enter western longitudes as their corresponding eastern equivalent, e.g. instead of entering 45W, which must be entered as `-45` as will be explained later, you can enter 315E, which is entered as `315`.

### Position and Angle Format

Positions are represented in degrees of latitude and longitude which can be entered either as *DD°MM'SS"* using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="abc" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/abc.png" valign="middle"> key combination or in decimal degrees *DD.ddddddd*. Northern latitudes are positive, so 14°45'21"N is entered as `14°45'21"`, while southern latitudes are negative, so 20.2321S is entered as `-20.2321`. Same with declination: N45.2345 is represented as `45.2345` while S12°51'03" is represented as `-12°51'03"`. Positive values of longitude greater than 180° will be converted to a negative value corresponding to the western longitude, e.g. 220 will be converted to -140.

Celestial navigation positions, declinations, corrections, hour angles, etc., are traditionally represented using degrees and decimal minutes to one decimal place, e.g. *DD°MM.m'*, but the calculator does not natively support that format. Decimal minutes must be converted to arc seconds which are equal to the decimal part of minutes multiplied by 6. For example, S24°8.4' must be entered as `-24°8'24"`. That being said, the program usually outputs values using decimal minutes.

### Date Format

Date values are represented using the native calculator format which is *YYYY.MMDD*. For example, April 23, 2026 must be entered as `2026.0423`.

### Time Format

Time values are represented in 24-hour format using the same format as angle degrees, i.e. *HH°MM'SS"*, using the <img alt="Shift" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/shift.png" valign="middle">-<img alt="abc" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/abc.png" valign="middle"> keys. For example 11:43:12pm is entered as `23°43'12"`.

### Dark Mode

The color theme used by the calculator can be set to Light or Dark mode on page 2 of the Settings menu. The program will adjust its display based on the theme set. When making observations during twilight hours, it is preferable to set the calculator to a Dark theme to preserve night vision. The screens below illustrate the display in dark mode.

![Dark mode example 1](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/darkmode0.png)&nbsp;&nbsp;&nbsp;
![Dark mode example 2](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/darkmode1.png)&nbsp;&nbsp;&nbsp;
![Dark mode example 3](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/darkmode2.png)

## Initialization

### Clearing Memory

The program keeps data about sights and lines of position in the calculator's memory, and that data is preserved when the calculator is turned off. Generally, you should clear the program's memory prior to any new fix. If you ever get an **Invalid Input** error, you likely inadvertently opened the **Sight Reduction** program for editing and need to clear the memory (see the **NOTE** in the [Confirming that Everything Works](#confirming-that-everything-works) section). To clear all program variables:

1. Highlight the **Sight Reduction** program and press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key
2. From the list of options, pick **RESET_SIGHTS** on the touchscreen or with the arrows and the <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> key. Click any key to dismiss the confirmation message.

![Resetting variables](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

### Setting the Time and Time Zone

The calculator has a pretty accurate internal clock that can be used to automatically record the time of observations. It should be set to a reliable external time source from time to time to ensure it is accurate. To set the calculator's internal clock and timezone:

1. Run the **Sight Reduction** program and pick the **SET_TIME** function and set the calculator's local time clock and timezone:

   * **Local time**: the local time to which to set the calculator. Enter a time a few seconds in the future and click the <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> soft key when your time source reads the time entered
   * **UTC Offset**: the number of hours ahead of or behind UTC. Use a positive value for locations East of Greenwhich and negative for West (e.g. -5 for New York standard time). Keep in mind that this offset changes with Daylight Savings Time (DST)

![Setting the time and timezone](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/settime.png)

## Planning Observations
It can be helpful to know which celestial bodies will be visible and where ahead of an observation session with the sextant so that the bodies to be observed can be selected ahead of time based on whether they meet certain a criteria for visibility based on their altitude and azimuth. The program shows, for a given date, all the bodies that meet the visibility criteria at morning and evening nautical twilight, as well as at a specified time during that day. Here's how it works:

1. From the programs screen of the calculator, select the **Sight Reduction** program and click the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key and click on the **SIGHT_PLANNING** function. An input screen will appear:

![Parameters for listing bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_input.png)

2. Fill out the observation parameters and visibility criteria:
   * **Date**: the date on which the observations will be made in YYYY.MMDD format
   * **Time**: an arbitrary time at which to show the visible bodies, in HH°MM'SS" format
   * **Latitude**: the latitude in degrees from which the observations will be made
   * **Longitude**: the longitude in degrees from which the observations will be made
   * **Altitude**: the minimum altitude in degrees of the celestial bodies to be included in the list
   * **Azimuth from**: the true heading in degrees of the beginning of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list
   * **Clockwise to**: the true heading in degrees of the end of a clockwise arc within which the azimuth of bodies must lie in order to be included in the list

3. It will take about 1-2 minutes to compute all the ephemerides. You will be prompted to press a key to show the results at the end of the calculation. The output will be shown in the Spreadsheet app with all times in local time (assuming **SET_TIME** was run to specify the time zone). It will include, in clockwise order of azimuth within the prescribed arc:
* Sunrise, sunset, civil twilight, and nautical twilight times
* Local time of Meridian passage at the specified longitude
* List of observable bodies (i.e. meeting azimuth and altitude constraints entered on the first screen) with, for each, the azimuth, true altitude (Hc), apparent altitude (Ha) (i.e. the one that a sextant with no index error and no dip would read), Greenwhich Hour Angle (GHA), declination (dec), semi-diameter in arc seconds of the body (if applicable), and rise and set times (if applicable), at 3 different times:
  * Morning nautical twilight: from morning Nautical Twilight Time to Civil Twilight Time (if there is a sunrise at that location), with body positions calculated at the midpoint of the twilight period, shown in parentheses
  * Evening nautical twilight: from evening Civil Twilight Time to Nautical Twilight Time (if there is a sunset at that location), with body positions calculated at the midpoint of the twilight period, shown in parentheses
  * The time specified in the input form
 
![List of bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_output.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![List of bodies](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/listbodies_output2.png)

## Reducing Sights
Performing a sight reduction is a straightforward process: 

1. Go to the Programs screen, highlight the **Sight Reduction** program and press the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key.

2. Reset all previous observations and calculations by running **RESET_SIGHTS** in the **Sight Reduction** program.

![Sight Reduction programs](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sightreductionprograms.png)

3. Enter a new observation: select **SIGHT** and press the <img alt="Enter" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/enter.png" valign="middle"> soft key.

4. The program can store up to 10 different observations, each resulting in a line of position, and they are accessed by an LOP register number from 1 to 10. Select an LOP register for this observation, let's say **1** for this first one, and hit the <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> soft key. LOP registers containing a translated LOP cannot be edited and, if selected for editing, will be treated as an empty sight that will overwrite the translated LOP. The source of a translated LOP can be edited but its corresponding translated LOP will not be updated. See [Running Fixes](#running-fixes).

The **Show Progress** checkbox simply causes additional computing messages to be displayed during the calculation processes and changes nothing to the results.

![Observation register selection](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input1.png)

5. The next screen captures the parameters of the observation:
   * **UTC Date**: the UTC date of the observation in HP Prime date format (*YYYY.MMDD*). The hint at the bottom of the window displays the current UTC time to help determine if the UTC date is different from the local date. The default value is the current UTC date.
   * **DR Lat**: the latitude of the dead-reckoning (DR) position in degrees at the time of the observation
   * **DR Lon**: the longitude of the DR position in degrees at the time of the observation
   * **Body**: a drop-down to select the celestial body being observed among a list of the Sun, Moon, 4 planets and 58 stars. For certain celestial bodies, the observed limb must also be selected. The **Pre-calculated sights** option allows entering the *Zn* (azimut) and *a* (distance) of the line of position directly instead of letting the calculator perform the sight reduction calculations (this is useful to plot lines of position that have been calculated some other way). The **Moon with tables** and **Sun with tables** options allow entering the values for declination and Greenwich Hour Angle manually based on the Almanac tables instead of using the built-in ephemerides.
   * **Artificial**: check this box if the observation was made on an artificial horizon. If that's the case, the sextant reading values entered must be the actual reading on the sextant, i.e. double the actual body height. When this box is checked, the index correction will be applied before dividing the reading by half and no dip correction will be applied regardless of the eye height or dip short values entered
   * **Average**: check this box to perform the observation averaging process described in the next step. Note: this checkbox is unchecked by default if the LOP register contains a previously entered sextant altitude. Checking it will overwrite the previously entered sextant altitude. If no previous value was entered, the checkbox is checked by default.

![Basic observation data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input2.png)  ![Selecting celestial body](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input2b.png)

6. On the next screen, enter the observation conditions which will be used to compute sextant altitude corrections:
   * **IC**: the index correction of the sextant in arc minutes, negative values for "on-scale" correction and positive for "off-scale"
   * **HE**: eye height from the horizon in feet (for dip correction)
   * **Dip short**: distance in nautical miles (nm) from observer where the horizon ends (e.g. the other side of a large lake), or zero if an infinite horizon is used as reference for the observation
   * **Temp**: the air temperature in degrees C (for refraction correction)
   * **Pressure**: the atmospheric pressure at sea level in millibars (for refraction correction)

![Observation correction data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input3.png)

7. If the **Average** option was selected, the program will prompt the user to enter sextant observations as they are made. It will show a screen asking to press any key when an observation is made and pause there until a key is pressed. (It might be useful to extend the Auto-OFF delay of hte calculator by setting the value of the *TOff* system variable to a longer delay. See [this link](https://www.hpmuseum.org/forum/thread-5664.html)):

![Press any key](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/avgproc1.png)

8. As soon as you've aligned the observed body with the horizon, hit any key or touch the touchscreen. This will note the time of the observation (hence why it is important to run **SET_TIME** regularly) and a screen prompting to enter the sextant reading will appear. **IMPORTANT: do not halve observations made on an artificial horizon and do not apply any dip or index corrections to the sextant reading, these corrections will be entered later.**

![Enter sextant reading](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/avgproc2.png)

9. The program will return to step 6 and allows entering as many observations of the same body as desired. When no more observations are needed, hit *Cancel* or enter `0` in the HS field and click *Ok*. If only one observation was entered, the program will skip directly to step 10 and use the time and sextant altitude values entered in Observation #1
  
10. If more than one observation was entered, the observations will be plotted on a Cartesian graph with time as the horizontal axis and sextant altitude as the vertical axis. The plot allows choosing among various best-fit curves using the soft keys at the bottom of the screen to pick the one most closely approximating the path of the celestial body in the sky: linear or quadratic regressions are available if 3 or fewer observations were made, and cubic or trigonometric regressions if 4 or more observations were entered. A red marker indicates a chosen value on the interpolated curve, which is at the midpoint of time range on the regression curve, unless an extremum exists within the time range, in which case that extremum is chosen. When done, hit the <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> soft key to confirm the selected interpolated point.

![Plot observations](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/avgproc3.png)![Plot observations](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/avgproc4.png)

11. The next input screen captures the time of the observation and the actual sextant altitude for the sight. If the observation averaging process was used, the fields will be pre-populated with the averaged values for time and angle and you can just click <img alt="Ok" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/ok.png" valign="middle"> to confirm it. Otherwise, enter the values for observation time and sextant altitude (and remember NOT to halve the sextant altitude if an artificial horizon was used). 

![More input data](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_input4.png)

12. The calculator will display the values for observed height *Ho*, Greenwhich Hour Angle *GHA*, declination *dec*, Local Hour Angle *LHA*, and the calculated height *Hc* of the body. Click **OK**

![Calculation results](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output1.png)

13. The calculator will then display the usual 4 parameters of the line of position: LOP register, distance *a* from the LOP either *TOWARD* or *AWAY* from the body, azimuth *Zn* to the body, and the DR position latitude and longitude as entered (no correction of DR position to an assumed position is necessary here because the calculator can easily handle fractional LHA and Zn). These parameters enable plotting of the line of position.

![LOP parameters](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output2.png)

14. Lastly, the calculator displays the equation for the line of position in a longitude (x) and latitude (y) Cartesian plane which can be used to plot it in a program. That equation is stored in the `F` register of the Function app of the calculator corresponding to the LOP register selected, e.g. LOP 1 will be stored in `F1`, which means they can be plotted using the calculator's Function app. (This step will be removed in a future version, it was originally used for debugging purposes.)

![LOP Equation](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/sr_output3.png)

## Running Fixes

In order to make a fix using two or more lines of position from observations taking at a different DR position, for example to make a fix based on a morning and an afternoon Sun sight while navigating, the earlier fixes need to be translated by the DR delta between those two positions. This is easily accomplished by running the **SHIFT_LOP** program. The first screen will prompt for the LOP that needs to be translated:

![Running Fix - Source LOP](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/runningfix1.png)

The next screen prompts to enter by what distance and bearing to shift the LOP. Enter the bearing in true degrees and the distance in nautical miles:

![Running Fix - Delta](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/runningfix2.png)

The next screen prompts for the LOP register in which to store the resulting translated LOP. You can select the same LOP as the source LOP, in which case it will be overwritten with the translated LOP and the original observation will be lost (which is usually fine), or another LOP register:

![Running Fix - Destination](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/runningfix3.png)

The calculator will output the magnitude of the translation in degrees of latitude and longitude.

![Running Fix - Ouptut](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/runningfix4.png)


## Making a Fix

Once 2 or more LOPs have been defined (i.e. 2 or more sights have been entered in separate LOP registers), a fix can be made either manually by visualizing the LOP plot or automatically by computing a center of LOP intersections.

### Manual Fix

A manual fix is made by visualizing the LOPs on a Cartesian plane with longitude as the horizontal axis and latitude the vertical axis. To do that, run the **Sight Reduction** program and select **PLOT LOPs**. This will open the calculator's Function app and a line of position will be plotted for each LOP defined in the **SIGHT** program. The calculator functions accessible through the soft keys can then be used to calculate the intersection of LOPs, etc., and the cursor can be used to manually find the centroid or some other position inside the "cocked hat" to make a fix. In order to determine which line color corresponds to which LOP, use the **Symb** key to view the color coding and the corresponding LOP equations, and use the **Plot** key to go back to the graph.

![Sample LOP plot](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/plot_lop.png)

### Computed Fix

Alternatively, the calculator can compute a fix based on LOPs. The computation varies depending on how many LOPs are defined:

  * 2 LOPs: the intersection of the 2 LOPs is the fix
  * 3 LOPs: the symmedian center, or Lemoine point, of the triangle formed by the 3 LOPs
  * 4 or more LOPs: the coordinate that minimizes the square of the error with each LOP based on the distance between the calculated coordinate and the shortest path to each LOP. This is achieved using derivatives of a function which is the sum of the squares of the distance of the coordinate to each LOP.

LOPs that were translated to a different LOP register are omitted from the calculation, but their translated destination registers are included.

To compute a fix, run the **Sight Reduction** program and select **COMPUTE_FIX**. The output will indicate which method was used to compute the fix and the longitude and latitude of the fix. In the screen shots below, we computed a fix after two sights, then entered a third sight and computed the fix again, and entered a fourth sight and computed the fix again:

![Fix with 2 sights](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/fix2.png)

![Fix with 3 sights](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/fix3.png)

![Fix with 4 sights](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/fix4.png)

If you have access to your actual position using a GPS or some other means to make a fix, you can compare the computed fix with your actual position. To do this, click the **Check** soft key at the bottom of the fix screen. You will be prompted to enter your actual position:

![Actual position input](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/fix4b.png)

Once your actual postiion is entered, the calculator will display the distance between the computed fix and the actual position:

![Fix error output](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/fix4b.png)

## Ephemerides
The program can show the Greenwich Hour Angle (GHA) and declination of the Sun, Moon, Mars, Venus, Jupiter, Saturn, and the 58 celestial navigation stars for any point in time between 1800 and 2200, as well as the corresponding azimuth and altitude from a specified geographical location. The semi-diameter of certain bodies will also be shown. A graphical representation of the ephemerides is available through the [Star Finder function](#star-finder) which is covered in the next section. To use this feature:

1. From the programs screen of the calculator, select the **Sight Reduction** program and click the <img alt="Run" src="https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/keys/run.png" valign="middle"> soft key and click on the **EPHEMERIDES** function. An input screen will appear:

![Ephemerides input screen](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/ephemerides_input.png)
  
2. Fill in the required information:
   * **Date**: the date of the ephemerides in YYYY.MMDD format
   * **Time**: the UTC time of the ephemerides in HH°MM'SS" format
   * **Latitude**: the latitude in degrees to calculate azimuth and altitude
   * **Longitude**: the longitude in degrees to calculate azimuth and altitude

3. The calculator will display several astronomical calculations such as Delta T, mean and true obliquity of the ecliptic, true GHA Aries, Moon phase (illumination %), UTC time of Meridian passage at the specified longitude, etc. along with the GHA, declination, azimuth, altitude, semi-diameter, rise and set times of all the celestial bodies:

![Ephemerides output screen](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/ephemerides_output.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Ephemerides output screen](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/ephemerides_output2.png)

## Star Finder
A plot of the sky with the 58 celestial bodies based on their ephemerides can be displayed by using the **STARFINDER** function of the **Sight Reduction** program. The input screen is the same as for the [ephemerides function](#ephemerides), with additional fields to specify the observer's gaze: initial center of the star finder view in terms of azimuth and altitude, and the initial field of view (which is the inverse of a zoom level):

![Star Finder](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/starfinder_input.png)

Upon submitting the form, the calculator will perform the ephemerides calculation for the selected date and time. At the end of the calculation, a graphical representation of the sky will be displayed. The view is a stereographic projection of the sky which preserves the angles between the celestial bodies and the shapes of constellations. The stars and planets are shown as blue dots if above the horizon or red dots if below the horizon. The center of the screen corresponds to the azimuth and altitude of the viewer and is displayed at the bottom of the screen. The following keys can be used to navigate the plot:
   * **Up/Down Arrows**: tilt view up/down
   * **Left/Right Arrows**: pan view left/right
   * **Touchscreen drag**: you can drag the view using the touchscreen drag gesture
   * **ESC** or **On**: exit the program

![Star Finder](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/starfinder.png)

While dragging or holding a key down, only the stars and planets will be redrawn. The grid lines will be redrawn when the keys and the touchscreen are released.

## Setting Default Index Correction

Whenever a new sight is entered, a value for the index correction of the sextant must be specified. A default value for the index correction can be defined using the **INDEX_CORRECTION** program. The value of the default index correction can either be entered directly or it can be calculated based on a measurement of the diameter of the Sun.

Start by launching the **INDEX_CORRECTION** program and choose either the *Direct* or the *Solar* method using the soft keys. At the end of the procedure, the value of the index correction for all sights that have no sextant angle entered will be set to the new default index correction value (i.e. the index correction of existing sights will not be changed).

![Index Correction options](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/index_correction.png)

### Direct Entry

When selecting the Direct soft key, the following input screen appears. Enter the default index correction in the field in decimal minutes (*MM.m*), with a negative value for an on-scale correction and a positive value for an off-scale correction.

![Direct Entry](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/index_correction_input.png)

### Calculation from Sun Diameter Measurement

Calculating the index correction from a measurement of the diameter of the Sun is accomplished by following the procedure described in [this document](https://www.starpath.com/online/celestial/solar_ic.pdf). The procedure assumes that the index correction is small enough such that the top measurement is on-scale and the bottom measurement is off-scale. The program briefly describes the measurements that need to be taken:

![Solar IC intro](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_intro.png)

Values for the *Below* and *Above* observations as read on the sextant, in decimal arc minutes (*MM.m*), can be entered in the input form. **Do NOT correct the off scale *Below* reading by subtracting it from 60, the program will do that for you. Use the value directly read on the instrument.**

![Solar IC input](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_input.png)

The program will display the calculated index correction result as well as the implied semi-diameter of the sun, which is then compared with the actual semi-diameter of the sun at the current time. This allows validating the inputs used before applying the calculated index correction to future sights.

![Solar IC output](https://github.com/placidanomaly/HPPrimeSightReduction/blob/main/img/solaric_output.png)

If the observed diameter of the Sun is close to the actual value, press the *Accept* soft key to apply the calculated index correction, or *Cancel* otherwise. It is recommended to run the procedure a few times to confirm the validity of the index correction. The mean value of several calculations can be entered using the [Direct Entry](#direct-entry) method.

# Future Improvements
The ephemeris calculations are usually accurate to within less than 0.1' of the values in the Almanac for the period 1800-2200 (subject to Delta T adjustments), but errors of up to 0.3' are sometimes seen. This is sufficient for most practical cases of celestial navigation but perfect precision would be better. The differences are still being investigated because the same program in Javascript from Henning Umland's web site seems to always output the exact same numbers as the Almanac. The possibility of a discrepancy in the code is one theory but a more likely one is that the lower number of significant digits in the calculator vs. a regular computer introduces rounding errors that add up in the lengthy calculations, but that has yet to be proven.

Instead of storing all sights as local data in the **Sight Reduction** program, we are considering making them global which would prevent their erasure when the program is open for editing. But that would mean that dozens of variables would pollute the global scope of the calculator. Comments on this would be welcome.

# Contact
This program was developed by [Charles Vaillancourt](mailto:charles.vaillancourt@gmail.com). I welcome comments and suggestions for improvement and will gladly review pull requests for inclusion into the program. And if you do try it, drop me a note to let me know how the installation and use of the program worked out for you, and if you were able to make a fix!
