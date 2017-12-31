# SPI-SREC-Bootloader
KCU105 SPI SREC Booloader

KCU105 SREC Bootloader Design
1)	To create the SPI SREC Design you need following blocks in your design
•	Microblaze processor
•	AXI Quad SPI
•	DDR4 SDRAM (MIG)
•	UART
•	Interrupt controller and System Reset

2)	Create a design in vivado with above components in the block design and run the block automation and connection.

3)	You can simply use the board automation to simplify the process of creating a design
For example, if you want clock in your design you can simply drag and drop the system clock from the board tab inside the vivado by doing this vivado would take care of all the constraints and you don’t need to apply the constraints in the XDC. For SREC bootloader you can drag and drop the DDR3SDRAM from the board tab.
 
Please make sure while creating the project you have selected the KCU105 board from the board tab and not the fpga part.
4)	After creating the design and running the block automation, your block design would look like below
                     
5)	Please create a design wrapper and run the implementation in vivado and let vivado generate the bitstream. Since you would use the board automation flow there will be no need of XDC constraints. Vivado would pick the constraints from the board file.
6)	After the bitstream generation, export the design to SDK file Export the design.
                     
Make sure include bitstream is checked.

7)	Open the SDK by File Launch SDK in vivado. 

8)	After the SDK is opened, next step would be to create the BSP, application and program the flash .Please follow the steps from step 2 from the below AR
https://www.xilinx.com/support/answers/64238.html

In the step 5, updatemem utility would run to combine the fpga. Bit file and an application (srec bootloader), this will create the Download.bit which would be used to program the flash.

9)	AR covers all the steps from creating the spi srec bootloader and an application loading and programming into the flash.

10)	You can try above steps for hello world, after this you can simply replace hello world application by your application elf.
11)	I have created the design on KCU105 by following all above steps, your output would look like below
 

12)	I will attach the design in SRM, if you would like to take a look. You can also directly program the flash by these files in that case just follow step 6 and 7 from the AR.
13)	After programming the flash, following things take place
Upon power on, FPGA configures itself from the SPI flash (Set the mode pins for SPI mode)
Microblaze runs the srec bootloader application which copies the application from 0x00600000 into a DDR memory on the board
After copying the application from the flash memory to DDR it executes the application from DDR memory. You can check the UART console in the above screenshot for the same.
