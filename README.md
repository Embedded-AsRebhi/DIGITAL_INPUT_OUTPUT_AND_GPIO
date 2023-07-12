# DIGITAL_INPUT_OUTPUT_AND_GPIO
During this exercise, we will need to write a program which inputs the status of the joystick on the application board, and  outputs them to the LEDs on the mbed LPC1768 board. We will learn in practice how to configure a General  Purpose Input Output (GPIO) peripheral at the register-level (low-level).

Before using the GPIO to interface with external pins, it has to be configured by writing to its internal registers:

 Direction register: 
The 32-bit direction register is used to control the direction of the 32-bit data. Setting a direction register bit to
1 indicates it is an output bit, and clearing to 0 will makes it an input bit. 
For example, if you want to write to bit[2] and output to the external pin, you will need to firstly write 0x04 to 
the direction register, or use shifting operation as follows:
DIR = (1<<2); //make bit[2] as output and other bits as input
Or 
DIR |= (1<<2); //make bit[2] as output while keeping other bits unchanged

 Mask register:
The 32-bit mask register can be used to mask out the bits that you do not wish to access (either for read or 
write operations). Setting a bit to 1 will mask that bit, and clearing a bit to 0 enables the bit to be accessible. 
For example, if you only want to change bit[2] while keeping other bits untouched, you will need to write 
0xFFFFFFFD to the mask register, or use shift operation as follows:
MASK = ~(1<<2); //mask all bits except bit[2]
Or
MASK &= ~(1<<2); //make bit[2] accessible and keep accessibility of 
 //other bits unchanged

  Input register: 
 This is a 32-bit register that keeps the value of the 32-bit input data.
For example, to read bit[2] of the 32-bit input data, you can use:
Input_data = ((INPUT & (1<<2)) >>2);
//Input_data=0x01 when bit[2] 
is //one, and 0x00 if bit[2] is zero

 Output set register : 
After configuring a bit to be an output, writing 1 to certain bits of this output set register will set the 
corresponding output bits to one. For example if you want output one to bit[2], you can write:
SET |= 1<<2; //set bit[2] and remain other bits unchanged

 Output clear register :
To clear an output bit to zero, you need to write 1 to the clear register (rather than writing 0 to the set 
register), for example to output 0 to bit[2]:
CLR |= 1<<2; //clear bit[2] and remain other bits unchanged
