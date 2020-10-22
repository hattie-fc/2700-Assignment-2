# 2700-Assignment-2: Satellite Computational Thermal Analysis

## Description
This program computes the temperature histories of the body and solar array of a satellite in low Earth orbit for 15 orbits. 
The program involves three main functions: 
1. irradiance(Ifull, tLEO, t): computes the irradiance encountered by the satellite
2. Tdot(t, T): computes the right hand side of the first-order differential equations developed from a lumped-mass heat-transfer equation. Takes irradiance(t) as an input.
3. rk3step(f, t0, y0, h): computes the approximate solution for the next time step using a third order Runge-Kutta scheme. 
These functions are written into a single program which outputs two plots and values for the maximum and minimum temperatures experienced by the satellite body and solar array. 
Using this information, thermal threats to the system may be analysed.

## Usage
To use this program, enter the required values for the input parameters. 
The program has a set of defult parameters listed in lines 25-62, however these can be adjusted by replacing the defult value with values specific to the problem at hand. 
Once these parameters are defined for the specific problem, the program requires no further input adjustments. 
For accurate results, values for the following parameters should be known in SI units: 
- mass
- average heat capacity
- emissivity
- geometries and cross sectional area's of components
- desired time step
- intial time and temperature values

If desired, the time step can be considered a variable. For example, set the time step in line 62 to 4 minutes (4*60 seconds), run the program and record the results. Then, run the program for increasingly smaller time steps and observe how the solution converges (for example: 4 minutes, 2 minutes, 1 minute and 0.1 minutes). 

### irradiance(Ifull, tLEO, t)
This is a simple function which should not require adjustment if the problem is a satellite in low-Earth orbit. The inputs (Ifull, tLEO, t) will remain constant for all problems in this situation. However, if the plot of irradiance may be customised to a desired time range in the following manor: 

- line 79: t_values = linspace(t0, tmax, num) ---> adjust t0 and tmax to minimum and maximum time range desired (seconds). For example: 
- line 79: t_values = linspace(t0, 2000, num) ---> will produced a 'zoomed in' plot to observe the periodic behaviour in more detail. 
Note: the maximum and minimum time values cannot exceed t0 and tmax specified in the input parameters.

### Tdot(t, T)
This function takes a current time value and a list of current temperatures. While used within this program, line 62 contains the input parameter for initial temperature: 
line 62: T0 = [300, 300] # Initial temperature of solar array and satellite body (K)
Where [300, 300] can be adjusted accordingly. 
Below this function are several print statements designed to test the function at the specified initial conditions. This allows the user to test the program is running as expected up to this point before proceeding to the final solution. 

### rk3step(f, t0, y0, h)
This is a general function which may be applied to any problem where a third order Runge-Kutta scheme can find a solution.
No adjustments to this function is necessary or advised. 

### Solution
The three functions above are employed to solve the system. No adjustment is required or advised except for the lines pertaining to the plot (lines 183 - 187):
- line 183: plot(ts, Tas, label = "T_a (K)")
- line 184: plot(ts, Tbs, label = "T_b (K)")
- line 185: xlabel('time, t (s)')
- line 186: ylabel('temperature (K)')
- line 187: title(f'Temperature variation of array and body for h={h}s')

If the plot of the values of only one component is desired, comment out either of lines 183 or 184. For example, if only the temperatures of the array are desired: 
- line 183: plot(ts, Tas, label = "T_a (K)") ---> temperature history of the array will be plotted with time
- line 184: # plot(ts, Tbs, label = "T_b (K)") ---> temperature history of the body WILL NOT be plotted with time

### Outputs 
As a defult, the program will automatically output all calculated results including: 
- a plot of the irradiance function over 15 orbits
- values for the Tdot(t, T) function for intial conditions as a test
- maximum and minimum temperature values for the solar array and satellite body at the specified time step
- a plot of the temperature variations of the satellite body and solar array
Note that the axis of the two plots are labelled for ease of interpretation. 

## Authors and Acknowledgements
Authors: 
Harriet Carlile (45832855)
Cameron Smith (45807922)

Date: 22.10.2020

### References: 
Wheatley, V. (2020). Assignment: Computational Heat Transfer. University of Queensland, School of Mechanical and Mining Engineering, Brisbane. Retrieved October 2020, from https://learn.uq.edu.au/bbcswebdav/pid-5330796-dt-content-rid-30673454_1/courses/MECH2700S_7060_61359/MECH2700-assignment2-2020.pdf
