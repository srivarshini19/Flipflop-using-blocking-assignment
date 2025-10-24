# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM 
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
timescale 1ns / 1ps


module SR_FF(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(s==0 && r==0)
q=q;
else if(s==0 && r==1)
q=1'b0;
else if(s==1 && r==0)
q=1'b1;
else
q=1'bx;
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module SR_FF_tb;
reg s,r,clk,rst;
wire q;
SR_FF uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
s=0;r=0;
rst=1;
#10 rst=0;
#10 s=1;r=0; //set
#10 s=0;r=0; //hold
#10 s=0;r=1; //reset
#10 s=1;r=1; //invalid condition
#10 s=1;r=0; //hold
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT
![SR FF](https://github.com/user-attachments/assets/da77cdce-1303-4ed7-a128-dd4fa0bc63bc)

------- paste the output here -------
---

### JK Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps

module JK_FF(J, K, clk, reset, q);
input J, K, clk, reset;
output reg q;
always @ (posedge clk) begin
if (reset == 1)
q=0;   
else begin
case ({J, K})
2'b00: q = q;     
2'b01: q = 1'b0;  
2'b10: q = 1'b1;  
2'b11: q = ~q;    
endcase
end
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
module tb_JK_FF;
reg J, K, clk, reset;
wire Q;
JK_FF uut (J, K, clk, reset, Q);
always #5 clk = ~clk;
initial begin
clk = 0; J = 0; K = 0; reset = 1;

#10 reset = 0;
#10 J = 1; K = 0;   
#10 J = 0; K = 1;   
#10 J = 1; K = 1;   
#10 J = 0; K = 0;   
#10 J = 1; K = 1;   
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT
![JK FF](https://github.com/user-attachments/assets/7305cf3d-b3cd-428c-a821-b24f09274e73)

------- paste the output here -------
---
### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps

module D_FF(D, clk, reset, Q);
input D, clk, reset;
output reg Q;

always @ (posedge clk) begin
if (reset == 1)
Q = 0;        
else
Q = D;        
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
module tb_D_FF;
reg D, clk, reset;
wire Q;
D_FF UUT (D, clk, reset, Q);
  always #5 clk = ~clk;

initial begin
clk = 0; D = 0; reset = 1;
#10 reset = 0;
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   

#20 $finish;
end
endmodule
```

#### SIMULATION OUTPUT
![D FF](https://github.com/user-attachments/assets/3fcc32ac-8d16-4ba8-9556-be8ec56aa21f)

------- paste the output here -------
---
### T Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module T_FF(T, clk, reset, Q);
  input T, clk, reset;
  output reg Q;
  always @ (posedge clk) begin
    if (reset == 1)
      Q = 0;          
    else if (T == 1)
      Q = ~Q;         
    else
      Q = Q;          
  end
endmodule
```
### T Flip-Flop Test bench 
```verilog
module tb_T_FF;
  reg T, clk, reset;
  wire Q; 
  T_FF UUT (T, clk, reset, Q);  
  always #5 clk = ~clk;

  initial begin
    
    clk = 0; T = 0; reset = 1;
    #10 reset = 0; 

    #10 T = 1;   
    #20 T = 0;   
    #20 T = 1;   
    #20 T = 0;  

    #20 $finish;
  end
endmodule
```

#### SIMULATION OUTPUT
![T FF](https://github.com/user-attachments/assets/0cfd1ba4-c0dd-4daf-9a44-7795fef3ba3b)

------- paste the output here -------

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
