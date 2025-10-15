# 32-BIT_ALU Simulation and Synthesis

## Aim:
Write a Verilog code for a 32-bit ALU supporting four logical and four arithmetic operations. Use case statements in behavioural modelling.
To verify functionality using the Test Bench, synthesize and analyse area and Power reports of a 32 Bit ALU design 

## Tool Required:
Functional Simulation: Incisive Simulator (ncvlog, nclaunch, ncsim)

Synthesise using Genus

## Design Information and Block Diagram:
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators.

<img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/1195efe3-e2dd-443c-8bf0-be1579c06533" />

#### Fig 1: Block Diagram of 32 Bit ALU

## Creating a Workspace:

Create a folder in your name (Note: Give folder name without any space) and create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_32bit.v)

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

#### a)	To verify the Functionality using the Test Bench

## Source Code – Using Case Statement :
```
module alu_32bit_case(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f;
output reg [31:0]y;
always@(*)
begin
case(f)
3'b000:y=a&b; //AND Operation
3'b001:y=a|b; //OR Operation
3'b010:y=~(a&b); //NAND Operation
3'b011:y=~(a|b); //NOR Operation
3'b100:y=a^b; //XOR Operation
3'b101:y=~(a^b); //XNOR Operation
3'b110:y=~a; //NOT of a
3'b111:y=~b; //NOT of b
endcase
end
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

## Creating a Test Bench:

Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_32bit_tb_case).

## Test Bench :
```
*module alu_32bit_tb_case;

reg [31:0]a;

reg [31:0]b;

reg [2:0]f;

wire [31:0]y;

alu_32bit_case dut(.y(y),.a(a),.b(b),.f(f));

initial

begin

a=32'h00000000;

b=32'h10101010;

#10 f=3'b000;

#10 f=3'b001;

#10 f=3'b010;

#10 f=3'b011;

#10 f=3'b100;

#10 f=3'b101;

#10 f=3'b110;

#10 f=3'b111;

#100 $finish;

end

endmodule*
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

## Functional Simulation:

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

![WhatsApp Image 2025-10-15 at 10 53 34_3748b886](https://github.com/user-attachments/assets/873d0e53-fcc8-4439-8813-621ff75a352f)



#### Fig 2: Invoke the Cadence Environment

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

![WhatsApp Image 2025-10-15 at 10 54 12_08801415](https://github.com/user-attachments/assets/73fb5345-32ef-46a3-af62-1d69c85c58a3)


#### Fig 3: Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option
![WhatsApp Image 2025-10-15 at 10 54 57_9bc21a90](https://github.com/user-attachments/assets/6960ace3-26fd-4902-943c-48443261862c)


#### Fig 4:cds.lib file Creation
Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below

#### Fig 5: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
![WhatsApp Image 2025-10-15 at 10 57 12_4fd0d469](https://github.com/user-attachments/assets/49fb3760-62d9-44b6-bb40-93d4e585458a)


#### Fig 6: Nclaunch Window

### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#### Steps for compilation:
1.	Create work/library directory (most of the latest simulation tools creates automatically)
   
2.	Map the work to library created (most of the latest simulation tools creates automatically)
   
3.	Run the compile command with compile options

i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code
Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation


#### Fig 7: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”
![WhatsApp Image 2025-10-15 at 10 57 37_34db9e11](https://github.com/user-attachments/assets/a04a0198-ac35-447b-8d6b-617c921e71db)


### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#### Steps for elaboration
– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.


#### Fig 8: Elaboration Launch Option

### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

![WhatsApp Image 2025-10-15 at 11 13 24_5e9dd2da](https://github.com/user-attachments/assets/6215821c-1ded-4fcd-a22f-2b705d15d4e5)


#### Fig 9: Design Browser window for simulation

![WhatsApp Image 2025-10-15 at 11 14 06_e2f2c490](https://github.com/user-attachments/assets/24349c49-2941-4808-8e7a-0e0a03f1a20a)

#### Fig 10: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/ed3ab4c5-e069-49d3-ac34-56fff3b42675" />


#### Fig 11: Synthesis RTL Schematic 

![WhatsApp Image 2025-10-15 at 11 18 16_51648fef](https://github.com/user-attachments/assets/c32127b0-fdae-41be-b37f-4a11bd576ef7)


#### Fig 12: Area report

![WhatsApp Image 2025-10-15 at 10 58 58_85a82042](https://github.com/user-attachments/assets/4b61769b-44d1-4e64-aeca-0af80e29df30)


#### Fig 13: Power Report

![WhatsApp Image 2025-10-15 at 10 59 20_8859acb8](https://github.com/user-attachments/assets/7cf616e8-d978-49a6-b455-bf05c688d765)


## Result
The functionality of the 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool. Additionally, the generic netlist of the 32-bit ALU was generated, and the corresponding area and power reports were analyzed and tabulated using Cadence Genus.
