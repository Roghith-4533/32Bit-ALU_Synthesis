# 32Bit-ALU_Synthesis
       
## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

![Screenshot 2025-05-20 104928](https://github.com/user-attachments/assets/7c5127d8-fd04-40a4-9f2d-ef7e49295372)

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

##Design Code
```
module ALU ( input [3:0] A, B,
input [2:0] ALU_Sel,
output reg [3:0] ALU_Out,
output reg CarryOut );
always @(*) begin
    case (ALU_Sel)
        3'b000: {CarryOut, ALU_Out} = A + B;
        3'b001: {CarryOut, ALU_Out} = A - B;
        3'b010: ALU_Out = A & B;
        3'b011: ALU_Out = A | B;
        3'b100: ALU_Out = A ^ B;
        3'b101: ALU_Out = ~A;
        3'b110: ALU_Out = A << 1;
        3'b111: ALU_Out = A >> 1;
        default: ALU_Out = 4'b0000;
    endcase
end
endmodule
```

##Testbench
```
module ALU_tb;
reg [3:0] A, B;
reg [2:0] ALU_Sel;
wire [3:0] ALU_Out;
wire CarryOut;

ALU uut (
    .A(A),
    .B(B),
    .ALU_Sel(ALU_Sel),
    .ALU_Out(ALU_Out),
    .CarryOut(CarryOut)
);

initial begin
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
    $finish;
end
endmodule

```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,
![Screenshot 2025-05-20 211305](https://github.com/user-attachments/assets/b348247a-f031-4572-86db-381d9beb0190)


• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh
![Screenshot 2025-05-20 104858](https://github.com/user-attachments/assets/6101b4e0-17eb-4e96-a4b4-a644cce1f3a3)


◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![vlsi 999](https://github.com/user-attachments/assets/77be1bb8-e69b-4e4f-9c65-1b3f9f7ba7c8)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![vlsi 000](https://github.com/user-attachments/assets/d07c2ae3-6727-4f96-b25a-25e3e30e1344)

#### Area report:
![Screenshot 2025-05-20 113916](https://github.com/user-attachments/assets/7d09f5cf-5a81-4c2f-be24-43e338f11f4a)

#### Power Report:
![Screenshot 2025-05-20 114016](https://github.com/user-attachments/assets/ff98542e-ca9c-4ddc-be32-85199a7cbc98)


#### Result: 
![vlsi77](https://github.com/user-attachments/assets/8f0134df-f059-4ee9-8a76-3dc904455000)


The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
