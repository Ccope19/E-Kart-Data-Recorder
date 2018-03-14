# E-Kart-Data-Recorder
This project is unlicenced and open-source to the public domain.  If one feels so inclined, they may cite the original creator (me) as my account username "Ccope19". 

**Schematic and PCB design (get gerber files here):**

 https://easyeda.com/Ccope19/E_Kart_Data_Recorder-3d7f9e403c7b447eae7c0b1731039f12 

**Purchasing, assembly, and programming instructions:** *(PLEASE UPDATE ME)* 
 https://www.instructables.com/ 

**Detailed Overview:**
The project is powered by the 4 lead-acid batteries that power the rest of the go-kart or any other power source between 7 volts and 59 volts.  This is done with a buck converter IC (LM2576HV) and capacitors and an inductor to smooth out the voltage.  This is then routed to all of the sensors, driver boards, data logger, and microcontroller.  The microcontroller is an ATMega328-P which is the same as an Arduino Uno R3 and requires a 16MHz crystal, 2 20pF ceramic capacitors, and a 10k pull-up resistor for the reset pin in order to function.  The microcontroller is programed through the ICSP headers on the data logger shield.  Once programmed, the microcontroller gets data from two switches and the hall effect sensor as well as the RTC (real time clock).  This info is then used to be written to the SD card or sent to the display drivers to be displayed on the 7-segment displays.  The displays are red, yellow, and green to represent the time, motor RPM, and speed respectively.

**Operation of Device:**
1)  Flip toggle switch to on position
2)  If device displays "no card" with blinking lights, insert SD card and hold down the clear button
3)  If the system continues with no SD card, the set-up portion of the code catches this and sets the device in an error state, requiring a reset.
4)  System now sets up and displays should go to ---- on all three and then 00.00, 0000, and 00.00 in order from top to bottom
5)  The program is now in it's "run w/o recording" mode so it will display the current motor RPM and cart speed without updating the clock or saving data.
6)  When the start/stop button is pressed, the device instantly detects this and switches modes after it finishes a cycle.  A cycle lasts however long it takes for the sensor to detect a magnet twice (a timeout should be added but this works for now)
7)  The device is now in it's "run and record w/ time" mode where it displays the clock from the start of the cycle as well as recording information in th format: "unix time, mm/dd/yyyy, hh:mm:ss  [clock], [RPM], [Speed]  " in a .CSV (common seperated value) file
8)  If the start/stop button is pressed, the device detects this and stops the clock as well as stopping the recording of data.  It then switches back to the default "run w/o recording" mode at the end of the cycle.  
9)  If the clear button is held down for on cycle (as described above in 6), the device performs the same task as 8 but also resets the clock to 00.00
