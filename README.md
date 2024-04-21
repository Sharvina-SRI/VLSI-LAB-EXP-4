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

## D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
## JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
## SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
## T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
## Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
## MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```

## OUTPUT WAVEFORM

### D Flip Flop

![D Flip Flop](https://github.com/RCKcharan10/VLSI-LAB-EXP-4/assets/117891438/0aeeb1ce-64b7-48e0-bcbd-efbf6bf0010d)

### JK Flip flop

![JK Flip flop](https://github.com/RCKcharan10/VLSI-LAB-EXP-4/assets/117891438/f58c6b39-81b3-400f-b2e6-5df43dd4f4ce)

### SR Flip Flop

![SR Flip Flop](https://github.com/RCKcharan10/VLSI-LAB-EXP-4/assets/117891438/c3f2b9c5-897f-48ef-b12d-2f446de70cb8)

### T Flip FLop

![T Flip Flop](https://github.com/RCKcharan10/VLSI-LAB-EXP-4/assets/117891438/5bae902d-bc9e-48f1-b32c-fdb06441a797)

## RESULT:
Thus the simulation and implementation of sequential logic gates is done and verified.
