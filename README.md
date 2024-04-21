# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

## AIM: 
To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

## APPARATUS REQUIRED:
Vivado 2023.1

## Procedure:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

Spartan6 FPGA

## LOGIC DIAGRAM

### SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


### JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

### T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


### D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


### COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
## PROCEDURE:
#### STEP:1  
Start  the Xilinx navigator, Select and Name the New project.
#### STEP:2  
Select the device family, device, package and speed.       
#### STEP:3  
Select new source in the New Project and select Verilog Module as the Source type.                       
#### STEP:4  
Type the File Name and Click Next and then finish button. Type the code and save it.
#### STEP:5  
Select the Behavioral Simulation in the Source Window and click the check syntax.                       
#### STEP:6  
Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
#### STEP:7  
Select the Implementation in the Sources Window and select the required file in the Processes Window.
#### STEP:8 
Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
#### STEP:9  
In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
#### STEP:10 
Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
#### STEP:11  
On the board, by giving required input, the LEDs starts to glow light, indicating the output.

## VERILOG CODE
```
DEVELOPED BY: SHARVINA SRI
REGISTER NUMBER: 212222060238
```
## SR FLIPFLOP:
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
## JK FLIPFLOP:
```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```
## T FLIPFLOP:
```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```
## D FLIPFLOP:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
## COUNTER:
#### Updown Counter:
```
module updown(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
#### Mod 10 Counter:
```
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
#### Ripple Counter:
```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```
## Output Waveform:
## SR FLIPFLOP:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/47473d68-9136-4e68-8027-82264d94eee9)
## JK FLIPFLOP:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/a284273b-00c4-4792-a0da-cd16cb6c7eac)
## T FLIPFLOP:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/7b0e8cc2-500d-4556-bab9-18cabfc8ecc4)
## D FLIPFLOP:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/d1367a46-fab5-4c66-84c9-1decdcb823cc)
## COUNTER:
#### Updown Counter:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/2e5bad24-7543-4bcc-8171-ed69ea581316)
#### Mod 10 Counter:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/8816b4c6-873d-463c-963e-f2b2484d228b)
#### Ripple Counter:
![image](https://github.com/Sharvina-SRI/VLSI-LAB-EXP-4/assets/162664906/e3e6d75b-67ef-4ae3-8146-ea76d920bfeb)

## Result:
Hence, the stimulation and synthesis of a SR flipflop, JK flipflop, T flipflop, D flipflop, Counter was run successfully by using Xilinx ISE.
