# Main_board_EAGLE_v_0_1

Eagle files for the main board version 0.1

This is the first version of the wooden haptics driver. This bord will accept 3 motors up to 3Amps each and 3 decoders. It has been designed to host ESCON motor drivers:

http://www.maxonmotor.com/maxon/view/product/control/4-Q-Servokontroller/438725

The same ESCON sockets can be used to connect any other DC motor driver if conencting to the propper pin connectors (PWR, motor out and PWM)

THis board can be used with and external DAQ (using the extension board) board or a mBed M3 Cortex:

https://www.sparkfun.com/products/9564

The elctronics are powerd up over USB but in order to power the motors it requires an external power supply 12v-48v, depending on the motors used. 
