# Design and Implementation of 48 bit SPI Protocol with clock frequency less than 1 MHz

The Serial Peripheral Interface (SPI) is a synchronous serial communication interface specification used for short-distance communication, primarily in embedded systems.The Serial-Peripheral Interface (SPI) protocol is one of the important bus protocols for connecting with peripheral devices from microprocessors. The complexity of the circuits has arised with the enormous advancement of IC technology. This paper represents a 3-wire SPI protocol (48-bit data) chip design for application-specific integrated circuit (ASIC) and its implementation with a constraint of clock frequency less than 1MHz. To accomplish compact, stable and reliable data transmission, the SPI is designed with Verilog HDL language and synthesized using the Genus tool in Cadence virtuoso software.

## Introduction:

Communication protocols are a formal definition of the formats and regulations of digital
messages. They are required to exchange messages within or between computing systems, and
they are significant in telecommunication systems and other systems Communications protocols
are implemented in hardware and software.
There are thousands of communications protocols that are used everywhere in analog and digital
communications. Computer networks cannot exist without them. We have presented the basics of
protocols such as Serial Peripheral Interface (SPI), Inter-Integrated Circuit (I2C), and Universal
Asynchronous Receiver/Transmitter (UART) driven communication. Later, SPI implementation
was presented.


## Serial vs parallel communication:
Electronic devices communicate with one another by transferring bits of data across wires that
are physically connected between them. Quick voltage changes are used to move bits from one
device to another. In a system operating at 5 V, a 0 bit is communicated as a short pulse of 0 V,
and a 1 bit is communicated by a short pulse of 5V. The bits of data can be transmitted either in
parallel or serial form. In parallel communication, the bits of data are sent all at the same time,
each through a separate wire.


![WhatsApp Image 2023-03-21 at 18 18 39](https://user-images.githubusercontent.com/127031157/226610823-207ccd8c-6da0-4c91-9477-f1ae20ff42fe.jpg)



![WhatsApp Image 2023-03-21 at 18 19 54](https://user-images.githubusercontent.com/127031157/226611091-55edd9c4-bcb0-4754-9434-0dc02a310541.jpg)



## Communication protocols
UART, SPI and I2C are the common hardware interfaces people use in microcontroller
development.
#### UART: 
UART (Universal Asynchronous Transmitter Receiver), this is the most common
protocol used for full-duplex serial communication. It is a single LSI (large-scale integration)
chip designed to perform asynchronous communication. This device sends and receives data
from one system to another system.● Both SPI master and slave have shift register
#### I2C:
The inter-integrated circuit or I2C Protocol is a way of serial communication between
different devices to exchange their data with each other. It is a half-duplex bi-directional
two-wire bus system for transmitting and receiving data between masters (M) and slaves (S).
## What is SPI?
MOSI (Master Output/Slave Input) – Line for the master to send data to the slave.
MISO (Master Input/Slave Output) – Line for the slave to send data to the master.
SCLK (Clock) – Line for the digital clock signal.
SS/CS (Slave Select/Chip Select) – Line for the master to select which slave to send data .

![image](https://user-images.githubusercontent.com/127031157/226615346-83a6b588-ca9d-4214-9442-92711b6d6a3e.png)


## Working of SPI 
#### The Clock:
The clock signal synchronizes the output of data bits from the master to the
sampling of bits by the slave. One bit of data is transferred in each clock cycle, so the speed of
data transfer is determined by the frequency of the clock signal. SPI communication is always
initiated by the master since the master configures and generates the clock signal.

The clock signal in SPI can be modified using the properties of clock polarity and clock phase.
These two properties work together to define when the bits are output and when they are
sampled. Clock polarity can be set by the master to allow for bits to be output and sampled on
either the rising or falling edge of the clock cycle. Clock phase can be set for output and
sampling to occur on either the first edge or second edge of the clock cycle, regardless of
whether it is rising or falling.

#### Slave Select
The master can choose which slave it wants to talk to by setting the chip select line(CS)
#### Multiple Slaves
SPI can be set up to operate with a single master and a single slave, and it can
be set up with multiple slaves controlled by a single master. There are two ways to connect
multiple slaves to the master. If the master has multiple slave select pins, the slaves can be wired
in parallel like this:


![image](https://user-images.githubusercontent.com/127031157/226616205-3e53264e-6610-4677-b556-f5fe14fb7ec1.png)


● Both SPI master and slave have shift register

● When the master wants to send the data to the slave, First it loads the data into its Shift
Register.

● The master then selects the destination. This is done by selecting the SS or CS line
associated with that slave.

● The serial Clock line is then enabled and one bit of the data is shifted on the MOSI line
with each clock pulse.

● Since the SPI protocol uses full duplex synchronous serial data transfer method, it could
transfer the data and at the same time receiving the slave data using its internal shift
register.

● From the SPI master and slave interconnection diagram on the right side You can see that
the SPI peripheral use the shift register to transfer and receive the data.



![image](https://user-images.githubusercontent.com/127031157/226616698-24df8c7d-dd9f-4112-b455-95a2a9ca8159.png)



● For example the master want to transfer Ob10001101(0x8E) to the slave and at the same
slave device also want to transfer the Ob00110010(0x32) data to the master.

● By activating the CS(chip select) pin on the slave device, now the slave is ready to
receive the data.

● Prior to a data exchange, the master and slave load their internal shift registers with memory data. Upon a clock signal, the master clocks out its shift register MSB first via the MOSI line.

● At the same time the slave reads the first bit from the master at MOSI, stores it into
memory, and clocks out its MSB via MISO.

● Continuously using the same principle for each bit, the complete data transfer between
master and slave will be done in 8 clock cycle.



![image](https://user-images.githubusercontent.com/127031157/226617294-37bc110e-617e-4cc6-ad8f-91894c38df0b.png)



## Pros and Cons:

### Advantages:
● No start and stop bits, so the data can be streamed continuously without interruption.

● No complicated slave addressing system like I2C.

● Higher data transfer rate (almost twice as fast) and consumes less power than I2C.

● Separate MISO and MOSI lines, so data can be sent and received at the same time.

● It supports full duplex communication.

### Disadvantages:

● Uses four wires (I2C and UARTs use two).

● No acknowledgement that the data has been successfully received (I2C has this).

● No form of error checking like the parity bit in UART.

● Only allows for a single master.

## Modes of SPI:
Clock polarity (CPOL) and clock phase (CPHA) are the main parameters that define a clock
format to be used by the SPI bus. Depending on CPOL parameters, SPI clock may be inverted or
non-inverted. CPHA parameter is used to shift the sampling phase.


![WhatsApp Image 2023-03-21 at 18 58 12](https://user-images.githubusercontent.com/127031157/226620567-397fe41a-e54e-4b64-bcd2-598393602297.jpg)


## Steps in Digital IC design


![image](https://user-images.githubusercontent.com/127031157/226621036-5c7d1a8f-944d-409c-933d-0c7939cfaf40.png)



Digital IC design is a procedural process that involves converting specifications and features into
digital blocks and then further into logic circuits. Many of the constraints associated with digital
IC design come from the foundry process and technological limitations.

## HDL coding:
HDL programming is the most fundamental step in Design IC design flow. A hardware
description language (HDL) is a programming language used to describe the behavior or
structure of digital circuits (ICs). HDLs are also used to stimulate the circuit and check its
response. There are various Hardware Description Languages such as Verilog, VHDL, and
system verilog. We have used Verilog to code SPI Protocol in our project. We use verilog to
describe a digital system as a set of modules.

## Pseudo Code:
Counter which keeps the count of the number of bits being transferred in one clock pulse and
MOSI (Master out slave in) has been defined. We started implementing the code of 16- bit data.
Later, it was extended to 48 bit data transfer.
Github link for the verilog code and it’s testbench of 48-bit SPI Protocol is attached below:
https://github.com/Saicharan004/SPI-Protocol
## Functional/gate simulation/verification:
After specifying the system in verilog, two things can be done: Simulation and Synthesis.
a) Simulate the system and verify the operation: It is just like running a program written in
some High-level language. It requires a test bench that specifies the inputs that are to be
applied and the way the outputs are to be displayed.
b) Use a synthesis tool to map it to hardware
In our project we have used EDA playground to verify the code first, later NCsim in Cadence has
been used. From the pictures shown below both the results are the same.
## Results:


![image](https://user-images.githubusercontent.com/127031157/226622227-a4beaaee-cab2-4560-a727-aca8930c914a.png)


![WhatsApp Image 2023-03-21 at 19 06 15](https://user-images.githubusercontent.com/127031157/226622845-8e169bfd-6bc1-49b7-bc5f-d583ff406bcf.jpg)


## Synthesis using Genus tool:
● We can create the best balance of power, performance, and area (PPA).

● Cadence synthesis provides an integrated flow that makes us understand the
architectural-level abstraction of the design and the detailed physical implementation
constraints.

● Till RTL Verification is a front end part (technically independent) we haven’t used any
libraries or tools.

● From synthesis it's related to the backend part. Synthesis is technologically dependent; it
gives netlist which will be helpful for the backend design.

● Synthesis converts hdl code to netlist code in the form of text file or circuit diagram
which has information about all the interconnections in it.

## RTL files:
The Register Transfer Level (RTL) is an abstraction for specifying a design's digital components
and often serves as the golden model in the design and verification flow. The RTL design is
usually captured using a hardware description language (HDL) such as Verilog or VHDL. RTL is
based on synchronous logic and contains three primary pieces namely, registers which hold state
information, combinatorial logic which defines the next state inputs and clocks that control when
the state changes.
## Writing TCL script files:
The Tool Command Language (TCL) format is used to write the commands in a file that is
understood by the tool. The command to run the GENUS Synthesis using SCRIPTS is
genus -legacy_ui -f genus_script.tcl

Here, example of two type of script file is given which are genus_script.tcl and
genus_script_dft.tcl

1. genus_script.tcl – this file is written to synthesize the Verilog file.

2. genus_script_dft.tcl – This file synthesizes the file with the MUX based scan chains

We use library files such as slow_vdd1v0_basicCells.lib and fast_vdd1v0_basicCells.lib for synthesis.
## DFT(design for test insertion):
DFT means testing synthesized netlist with testbench. It is not considered to be an important step
in designing.
## Results after synthesis:


![WhatsApp Image 2023-03-21 at 19 12 43](https://user-images.githubusercontent.com/127031157/226624516-56b83382-69c0-4c9a-9e90-e9fd9b88a054.jpg)


![WhatsApp Image 2023-03-21 at 19 14 08](https://user-images.githubusercontent.com/127031157/226624908-a9943083-66a9-468b-9147-3966c2b99024.jpg)


## Timing, Power, Qor reports:
### Static Timing Analysis Report:

```
Generated by: Genus(TM) Synthesis Solution 20.12-s150_1
Generated on: Mar 21  07:11:41 pm
Module: spi_state
Operating conditions: PVT_0P9V_125C (balanced_tree)
Wireload mode: enclosed
Area mode: timing library
Path 1: MET (8524ps) Setup Check with Pin MOSI_reg [0]/CK- >D
Group: clk
Startpoint: (R ) state_reg [1]/CK
Clock: (R ) clk
Endpoint: (R ) MOSI_ reg [0]/D
Clock: (R ) clk
Capture Launch
clock Edge :+ 10000 0
Src Latency :+ 0 0
Net Latency :+ 0 (I) 0
Arrival := 10000 0
Setup :- 118
Uncertainty :- 10
Required Time:= 9872
Launch Clock :- 0
Data Path :- 1348
Slack := 8524
```
####Path1: 
It tells whether the path has met or violated the timing.
In the SPI Protocol case the path has met the timing constraint i.e. The check is passed
The report gives information about startpoint and endpoint .

####Startpoint : state_reg[1] got triggered by clock CK.

####Endpoint: MOSI_reg[0] got triggered by D.

####Source latency : It is the delay from the clock source to clock definition pin in the design.
####Network latency : It is the delay from the clock definition point to the register clock pin.
From the Timing report Src latency and Net latency for both launch and capture flop is 0 which
means that there are no delay elements in the path.

####Data Arrival time: The time required for data to travel through the data path.

####Required time: The time taken for the clock to traverse through the clock path.

####Slack: It is the difference between achieved time and the desired time for a timing path. For a
timing path slack determines if the design is working at the specified speed or frequency.

From Spi protocol report, Slack is 8524 (slack=Required time - Data path time = 9872-1348 =
8524 > 0)
Positive slack in case of setup means design is working at the specified frequency and it has
some margin as well i.e. No Setup Violation.
We can’t exactly predict whether the constraint has been met or not just from the timing reports
after synthesis. Physical design has to be implemented to know the right predictions


![WhatsApp Image 2023-03-21 at 19 21 53](https://user-images.githubusercontent.com/127031157/226627054-3cf1881b-89f8-440a-8628-8c3e588ef705.jpg)


In the report shown above, these are probably the maximum path delays i.e. worst case delays.

####Timing Arc: Static timing analysis works on the concept of timing paths. Each path starts from
either primary input or a register and ends at a primary output or a register. In-between, the path
traverses through what are known as timing arcs.

####Fan-out: Fan-out is the number of equivalent inputs that can be safely driven by one output.In
the timing analysis report fanout has a minimum value of 30. So all the Timing points are
capable of handling inputs.

####Cell: It’s like a gate

####Arrival: It's the cumulative delay of each cell.

####Trans delay: It is the delay between 2 transactions in SPI communication.
####Trans delay should be less so that time is not wasted in propagating.

## Power Analysis:

```
Category Leakage   Internal   Switching   Total  Row%
Memory   0.00E+00  0.00E+00  0.00E+00  0.00E+00  0.00%
Register 1.31E-09  2.59E-06  1.81E-07  2.77E-06  61.25%
Latch    0.00E+00  0.00E+00  0.00E+00  0.00E+00  0.00%
Logic    3.29E-09  1.01E-06  5.77E-07  1.59E-06  35.17%
Bbox     0.00E+00  0.00E+00  0.00E+00  0.00E+00  0.00%
Clock    0.00E+00  0.00E+00  1.62E-07  1.62E-07  3.58%
Pad      0.00E+00  0.00E+00  0.00E+00  0.00E+00  0.00%
Pm       0.00E+00  0.00E+00  0.00E+00  0.00E+00  0.00%
Subtotal 4.60E-09  3.60E-06  9.20E-07  4.53E-06  100.00%
Percentage 0.10%   79.58%    20.32%    100.00%   100.00%
```

#### Leakage power: 
The power consumed by the sub threshold currents and by reverse biased diodes
in a CMOS transistor is considered as leakage power. Leakage power is the small amount of
power. From the report it is contributing just around 4.6 nano watts i.e. 0.1% of the total power
consumption which is sustainable.
#### Internal power: 
It is any power dissipated within the boundary of a cell. During switching, a
circuit dissipates internal power by the charging or discharging of any existing capacitances
internal to the cell. Internal power would be more compared to other powers like switching and
leakage power. From our report internal power contributes to 79.28% (i.e.3.6 micro watts) of the
total power consumption.
#### Switching Power: 
Switching power of a driving cell is the power dissipated by the charging and
discharging of the load capacitance at the output of the cell. The total load capacitance at the
output of a driving cell is the sum of the net and gate capacitances on the driving output.
Switching power contributes to 20.32% (i.e. 0.92 micro watts) of the total power.
Power consumption by the model should be as low as possible.
#### Total Power: 
It is the summation of leakage, internal and switching power.
In this report we have Total Power for each category. Summation of total power of each category
gives the SubTotal Power. We can also express it in percentile form.
Usually, if the total power is in milli or higher watts the power consumption is termed to be
more. We find that the total power summed to 4.52 micro watts which is low. Hence we can say
that the model is better and there’s no contradiction.
#### Black Box Testing: 
It is a testing technique where no knowledge of the internal functionality and
structure of the system is available. This testing technique treats the system as a black box or
closed box. The tester only knows the formal inputs and expected outputs, but does not know
how the program actually arrives at those outputs.
Testing helps to identify vagueness and contradictions in functional specifications.
Here in the black box analysis power due to each category is 0 it implies there is no contradiction
and vagueness in functional specification.
#### QOR Analysis:
It generally covers improvement and consistency in the performance of integrated circuits. QoR
covers logical combinational blocks (logic gates) to measure the performance of backend eda
tools.

```
Timing
Clock Period
clk 10000.0
Cost
Group
Critical
Path Slack
TNS Violating
Paths
clk 8523.6 0.0 0
default No paths 0.0
Total 0.0 0
Instance Count
Leaf Instance Count 112
Physical Instance count 0
Sequential Instance Count 10
Combinational Instance Count 102
Hierarchical Instance Count 0
Areas
Cell Area 228.798
Physical Cell Areal 0
Total Cell Area (Cell +Physical ) 228.798
Net Area 0
Total Area (Cell +Physical +Net ) 228.798
Max Fanout 12 (counter [0])
Min Fanout 0 (n_101)
Average Fanout 2
Terms to net ratio 2.6886
Terms to instance ratio 4.0089
Runtime 370.368029 seconds
Elapsed Runtime 29041 seconds
Genus peak memory usage 1318.92
Innovus peak memory usage no_value
```

Leaf Instance Count :
Leaf cells are cells that can't be broken down any further. Like AND gates and INV gates. These
take up real area on the chip die
Sequential Instance count :
A summation of the sequential cells in the design: Flops, latches, etc.
Combinational instance count:
The non-sequential cells: NANDs, BUFs, etc.
Hierarchical instance count :
Hierarchical instances aren't physical cells but named logical partitions of the design.
## Net Area:
The net area is probably a figure relating to the amount of routing resources used. It is defined in
the technology section of the library you're using and it's just an estimate of detailed routing
information that isn't available just after synthesis.
Total Area:
It's the sum of the standard cell area, macro and memory area.
## Physical Design:
### Floorplanning and Partition:
Floorplanning is the process of identifying structures that should be placed close together, and
allocating space for them in such a manner to meet the conflicting goals of available space ,
required performance.
Based on the area of the design and the hierarchy, a suitable floor plan is decided . Floorplanning
takes into account the macros used in the design, memory, other IP cores and their placement
needs, the routing possibilities, and also the area of the entire design. Floorplanning also
determines the IO structure and aspect ratio of the design.
The floorplan aspect ratio was set in order to fit write and read buses at the bottom of the IP. This
aspect also aims to facilitate the addition of PAD cells, considering that the top side groups every
output pin.


![WhatsApp Image 2023-03-21 at 19 34 02](https://user-images.githubusercontent.com/127031157/226630820-b00e30d3-ffde-4b6c-92bb-0971be00d09e.jpg)


Partitioning is a process of dividing the chip into small blocks. This is done mainly to separate
different functional blocks and also to make placement and routing easier.
### Placement:
Placement is the process of finding a suitable physical location for each cell in the block.
Tool only determines the location of each standard cell on the die.
Placement optimizes the design in addition to placing the standard cell that is present in the
synthesized netlist.


![WhatsApp Image 2023-03-21 at 19 41 59](https://user-images.githubusercontent.com/127031157/226633729-336e540c-b767-4640-af8f-85df95e5fb50.jpg)


## Clock Tree Synthesis
Clock Tree Synthesis is a technique for distributing the clock equally among all sequential parts
of a VLSI design. The purpose of Clock Tree Synthesis is to reduce skew and delay. Clock Tree
Synthesis provides the placement data as well as the clock tree limitations as input. Clock Tree
Synthesis (CTS) is the technique of balancing the clock delay to all clock inputs by inserting
buffers/inverters along the clock routes of an ASIC design.
## Routing
Routing is the stage after CTS where the interconnections are made by determining the precise
paths for each nets. This includes the interconnection of the standard cells, the macro pins, the
pins of the block boundary or the pads of the chip boundary.


![WhatsApp Image 2023-03-21 at 19 46 10](https://user-images.githubusercontent.com/127031157/226634341-f880e4bd-ff55-4f24-9fc5-e9762836c0cb.jpg)


## Conclusion:
A robust and simple SPI interface design was described in this paper. To accomplish compact,
stable and reliable data transmission, the SPI is designed with Verilog HDL language and
synthesized using the Genus tool in Cadence virtuoso software.
This work does not cover the whole process necessary to have a guarantee of a fully functional
circuit, but, at least it has introduced and instigated the search for the right practices for logical
and physical synthesis.
## References:
1. https://www.circuitbasics.com/basics-of-the-spi-communication-protocol/
2. https://focuslcds.com/serial-vs-parallel/
3. http://www.elecdude.com/2013/10/spi-verilog-code-master-slave-code-with.html
4. https://semiengineering.com/knowledge_centers/eda-design/definitions/register-transfer-level/
5. http://aboutme.samexent.com/classes/spring09/ee5327/Synlab7_S09.pdf
6. https://en.wikipedia.org/wiki/Physical_design_(electronics)
7. https://chipedge.com/what-is-clock-tree-synthesis
## Mentor
1. Neha Sayyad
## Mentees
2. Kandula Sai Charan

3. Mohammed Moin Abubakar

4. Venkatesh Naik Ajmeera
