Demonstrates the TCS230/TCS3200 Color Sensor Recognition Module using Energia and the RGB LED on the MSP432 LaunchPad.

See the wiki for a photograph of the sensor and examples of output.  The pin connections and further explanation are given inside the code.

Don't expect a whole lot from this sketch (or the TCS3200 variants for that matter).  It can recognize primary colors and simple mixes.  This sketch cannot display white, black, grey, etc.  The sensor output changes, sometimes dramatically, with changing incident light, material reflectivity, material orientation, size, distance, your individual sensor, etc.

The sensor works by reading light from photodiodes and gives an output for clear, red, green, and blue.  The output is in the form of a square wave with color a function of the wavelength (see datasheet).  The shorter the pulse, the higher the incidence of that color. The
sensor has different responsiveness to different wavelengths and this must be adjusted for.

This sketch uses pulseIn() to measure the frequency for each color and then adjusts for frequency responsiveness with an empirical factor, Rx.  Factors were developed using colored "card" paper.  Empirically, it also appeared that subtracting the clear reading out from each color helped.  The colors are then sorted to determine which colors are the primary contributors and adjusted  so they looked reasonable on a scale of 0 to 255.  It is implied by this algorithm that the colors in the calibration sample are mostly made of two colors with one dominant color.

Try adjusting the values Rc, Rg, Rb, and Rg first if you are not getting good results.  After that, try adjusting the factors/algorithm in the scaling section.

This sketch was also tried on the MSP430F5529 and it "worked" but gave poor results, probably due to pulseIn() inaccuracies in the F5529 implementation.  A better approach would be to use a timer and count interrupts.
