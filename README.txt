Initialization:

Create an instance of the pulsar object by giving it the full pathname to the pulsar fits file downloaded from https://gammaray.nsstc.nasa.gov/gbm/science/pulsars.html.  These will be the new fits version.  All the information contained in the fits file is now available in the pulsar instance.  All the data and orbital elements are available through the class variables.

eg.

source = pulsar('/Users/pulsar/monitor/Web_page/fits/gx301m2.fits')

To look at the parameters in this history invoke the source.printinfo() method.  It takes no parameters.

To make a nice plot of the frequency and pulsed flux just invoke the source.plot() method.   All plotting ranges are adjustable with keywords in the source.plot() method call: tmin,tmax,fmin,fmax,amin,amax, where t is time, f is frequency, a is pulsed flux amplitude.  The vertical plot range will always be set to the default tmin and tmax unless you specify the range in the call to source.plot().

The 'X' range can be independently set by changing the source.tmin or source.tmax or using the keyword tmin and tmax in the source.plot() call. The 'Y' range can only be independently changed with keywords in the source.plot() call.  

You can also plot the pulse profile near a given MJD in the 8-12 keV band (channel 0), 12 - 25 keV band (channel 1), and 25-50 keV band (channel 2).  

First identify the time and energy channel that you would like to see the pulse profile.  The method will choose the  pulse profile that is detected and just after or at the time you selected.

source.profile(59200.0, 1) 

This will generate the light curve for the pulse profile using the number of significant harmonics and store them in the class variables: source.phase_sig, source.lc_sig and source.lc_sig_error.  It will also generate a light curve using 10 times the harmonics to guide the eye and creating a smooth curve.  They are stored in the class variables: source.phase and source.lc.  There are no errors on the source.lc.  You can also center the profile at phase zero.  This essentially shifts the lowest phase bin to phase zero.  Just set the source.shift_zero = ‘yes’ or you can do it in the call to the method: source.profile(59200.0,1,center = ‘yes’).  Default is 'no' but once set 'yes' it will remain until unset. 

To plot the profile invoke the plot_prof() method.

An advanced feature is the source.binary_beta() method which takes a barycentered time array and calculates the velocity/c away from the observer given the ephemeris stored in the source.vel.  This may be used for adding back the orbital corrections performed after a search and/or testing a new orbital model.    