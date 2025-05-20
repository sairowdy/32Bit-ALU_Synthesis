# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

![image](https://github.com/user-attachments/assets/87d21779-474f-4455-8f50-64c7bdacf480)


◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

**Design code**:

module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output reg CarryOut );

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

**TestBench:**

module ALU_tb; reg [3:0] A, B; reg [2:0] ALU_Sel; wire [3:0] ALU_Out; wire CarryOut;

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

### Step 2 : Performing Synthesis

The Liberty files are present in the library path,


• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

![Screenshot 2025-05-20 114313](https://github.com/user-attachments/assets/14674925-a0fa-4e44-8e9d-a807ee9b1794)


• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :

![image](https://github.com/user-attachments/assets/c8d9675d-5719-4eae-a933-7c255a665276)

#### Area report:

![image](https://github.com/user-attachments/assets/5d5d122f-0811-4dfc-99ff-557f01bfa64b)

#### Power Report:

![image](https://github.com/user-attachments/assets/c401d6ee-d26c-4b08-b5fc-59c2661d54b5)

#### Result: 

![image](https://github.com/user-attachments/assets/84e06b65-3cb0-4b32-a471-7bda282db820)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
