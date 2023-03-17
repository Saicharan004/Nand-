# Nand-Flash-Memory

As a semiconductor memory device capable of nonvolatile data storage even after removing the power supply, NAND flash has gained popularity in a variety of applications, like removable memory cards for portable devices, MP3 players, digital still cameras, and mobile handsets. The emerging multi-media applications demand for higher density and lower cost/MB, and drive the continuous process technology shrink and the MLC (multi level cell) technology adoption. Nevertheless, the narrower line pitch due to process technology shrink may induce severer cross interference between memory cells. No matter the requirement for multiple energy states also leaves MLC technology with a lower margin of error to read the bits.

## Abstract

Since the NAND flash is operated through page (e.g. 2 Kbytes) programming and block (e.g. 128 Kbytes) erasing to satisfy the fast data transfer rate for mass data storage, an intrinsic random bit error makes the whole block be marked as “bad” and can no longer be utilized. Once the number of bad blocks exceeds a certain value that the controller chip can manage, the NAND flash chip is declared fail. 

## Functionalities of a NAND Controller

A NAND Controller is required to handle the bit errors, the bad blocks, maintaining the high data accessing speed, flash memory management, etc. The appropriateness of a NAND controller can enhance the reliability and increase the endurance cycles of the flash memory. In addition, the system performance and product lifetime can also be improved by incorporating an excellent NAND Flash Controller in the NAND Flash Storage Systems.

## Systolic Array Architectures

The Systolic Array architecture has been applied to the regular and iterative VLSI architecture, like RS encoders and decoders, and showed good performance [10]. The
systematic design approach of a Systolic Array Processor can make the circuit design easy for implementation and do the pipelining to fit the system level design specifications. In this paper, we presented a t-EC w-bit Parallel BCH ECC code with incorporating the Systolic Array architecture. The good performances were shown by the real chip realization.

## The Controller Architecture
The functional block diagram of the NAND Flash Controller was shown in Figure 1. The major functions of the Controller can be divided as: 

1. The t-EC w-bit Parallel BCH ECC Circuit,
2. The Code-Banking structure and Firmware In- System Programmable (ISP), 
3. The Defect Management and Wear-leveling Algorithm, and 
4. The Dual Channel and Multi- Buffering mechanism. 

The ECC Circuit was designed here to enhance the data integrity and reliability of the data stored in the Flash memory. The Code-banking structure for the Micro-controller complying with firmware ISP function can provide the firmware upgrade to support various kind of Flash memory. 

The Defect Management Algorithm can increase the yield of the Flash memory and prolong the product life cycle by replacing the defected (Bad) block with the reserved virgin (clean data) blocks. The Wear-leveling Algorithm was also introduced to prolong the product life cycle by preventing the Flash memory blocks from un-balanced usage. The Dual Channel and Multi-Buffering mechanism was designed to increase the data transfer rate at the Flash memory side and to fit the maximum bandwidth of the host-side interface bus.

![WhatsApp Image 2023-03-16 at 14 22 30](https://user-images.githubusercontent.com/127031157/225585123-35fd0a27-6540-4b58-9e9a-1f108aa87d8c.jpg)

The t-EC BCH ECC Code Construction A t-EC BCH ECC code can be constructed through the procedures shown in Figure 2.
![WhatsApp Image 2023-03-16 at 15 42 22](https://user-images.githubusercontent.com/127031157/225585582-3a7613a7-2dd4-4c06-a8ff-7bb01dafddcb.jpg)


Based on the general basic equation of a t-EC w-bit parallel BCH code, the basic operation module for the matrix array can be constructed by two AND gates and two
XOR gates. The coefficients ai’s are determined by the Generator Polynomial or the Syndrome Generator Polynomials of the BCH code. To complete the matrix equation (4) by the basic operation module, an Array Architecture is adopted. 

The Array Architecture of the n-bit input data stream for the BCH Generator Polynomial or Syndrome Generator Polynomials is shown as in Figure 3.
![WhatsApp Image 2023-03-17 at 10 10 56](https://user-images.githubusercontent.com/127031157/225814658-0ddd23b0-cbe3-42b3-9994-d6682f69a035.jpg)

The Code-Banking and various NAND Flash Memory Support The architecture for the Code-banking was shown in Figure 4. 

The Boot ROM was the Masked Read Only
Memory which stored the Boot codes for the Microcontroller
in Booting. By the Code-Banking architecture, the
whole system firmware can be separated by several banks,
Bank Code #0, 1, …, n. The Banked Codes will be executed
Bank by Bank when loaded by the Code Loader to the Bank
RAM. The System Firmware of the micro-controller can be
upgraded from the Host side.
To support the various kinds of the NAND Flash
memory in a controller, a specified Flash Parameters was
created to record some system operated parameters of the
NAND Flash memory. The Table was started by a Start-Tag,
and ended by an End-of-Table Flag. The useful parameters
such as: Total Capacity, Total Physical Blocks, Pages per
Block, etc. With the Code-Banking architecture and the
Specified Flash memory parameters, the various kinds of
NAND Flash memory can be supported in the same controller chip and be accessed in an optimal way
respectively.
![WhatsApp Image 2023-03-17 at 10 16 30](https://user-images.githubusercontent.com/127031157/225815069-78df4f01-f62f-4876-82c8-48cb25ccefb3.jpg)
THE DEFECT MANAGEMENT AND WEARLEVELING ALGORITHMS
Since the density progressing of the NAND Flash
memory, the closer the bit lines and the denser of the bit cells
caused some of the Flash memory blocks defected. The
defected Flash memory block which cannot be used or
accessed by the Controller is called the Defected Block, or
Bad Block. To increase the yield of the Flash memory, the
Defect Management in the NAND Flash Controller was
necessary. In general, the Defect Management was handled
by the designed sub-routines of the system firmware. In
Figure 5, a typical defect management method was shown.
The Defected Blocks which cannot be accessed was replaced
by some reserved good blocks via a Table, called the Defect
Management Table. When in the production stage, the
original defected Blocks will be scanned and replaced by the
reserved good blocks. Through the replacement of the
original defected blocks, the flash memory become useful
even if it contains defected blocks. This process for defect
scanning and replacement in the production stage is so called
the Static Defect Management. When the flash memory
being used in the usage stage, there is still the probability to
meet some normal blocks become defected. This
phenomenon usually happened in the Programming or
Erasing process, which can be identified by the Failure report
from the NAND Flash memory, or it can be checked by read
data back and compare after the user data page programmed.
The defected blocks detected during the normal operation
need to be managed as well. Since the defect management
was processed during the normal operation in usage phase,
the method is so called the Dynamical Defect Management.
