# PAPRA PCB Firmware setup

To use this repo, you will need a built PAPRA pcb, either the surface mount version or the thruhole version.  Check this repo for more information:

https://github.com/tetrabiodistributed/papra-pcba

and also check this out for build instructions for the thruhole board:

https://tetrabiodistributed.github.io/papra/

# Once I have a built board, what then?

Now you need to know what kind of fan you're pairing the board with.  The current firmware has three different sections for fans, like:

```C++ 
// MAP FOR CUI 154 BLOWER
// Limits the min pot value     Voltage   Min PWM Percentage
// const int minPWMfull = 108;  // 11.85V      69     >77%
// const int minPWM75p  = 112;  // 11.10V      72     >54%
// const int minPWM50p  = 115;  // 10.62V      77     >33%
// const int minPWM25p  = 120;  // 9.75V       88     >10%
// const int minPWM10p  = 250;  // 8.40V      110     >0%
// These values were determined emperically by adjusting the input voltage and dialing the PWM down until motor stall

// MAP FOR NM33GA-12Q-AT BLOWER
// Limits the min pot value     Voltage   Min PWM Percentage
//const int minPWMfull = 10;  // 11.85V      69     >77%
//const int minPWM75p = 11;   // 11.10V      72     >54%
//const int minPWM50p = 15;   // 10.62V      77     >33%
//const int minPWM25p = 20;   // 9.75V       88     >10%
//const int minPWM10p = 25;   // 8.40V      110     >0%
// These values were determined emperically by adjusting the input voltage and dialing the PWM down until motor stall

// MAP FOR SEEED ESP32-C3 SANYO BLOWER
// Limits the min pot value     Voltage   Min PWM Percentage
const int minPWMfull = 219;  // 11.85V      69     >77%
const int minPWM75p = 222;   // 11.10V      72     >54%
const int minPWM50p = 223;   // 10.62V      77     >33%
const int minPWM25p = 225;   // 9.75V       88     >10%
const int minPWM10p = 232;   // 8.40V      110     >0%
```

These values allow the potentiometer to be adjustable throughout the full range for each of the different fan types.  Right now, the code is set for the SANYO blower, since that particular fan has what we've found as the best combination of battery life and output pressure/flow (ie, it meets or exceeds what we need for flow while still having multiple hours of battery life).

Once you have the board built and attached, you should be able to flash using either ino module (thruhole for the thruhole board, surface for the surface mount board).

# papra-pcb-firmware for surface mount boards

Firmware is intended to be loaded on this PCB: https://github.com/tetrabiodistributed/PAPRA-PCB

Use the following arduino settings, change the chip to match the one you are using.

![image](https://user-images.githubusercontent.com/57600622/120357153-fc25b500-c2b9-11eb-8603-38b121836ca3.png)

Note: for ATtiny204 and ATtiny214 have 2K flash memory for program space. The preprocessor for TWOKFLASHCHIP must be uncommented prior to compiling. See Line 9.
