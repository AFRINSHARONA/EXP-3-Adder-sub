# EXP-3-Adder-sub
## Design and Verification of Half Adder and Half Subtractor
### Aim
To design and verify basic one-bit arithmetic circuits using Verilog HDL.
### Theory / Synopsis
A Half Adder adds two single-bit binary numbers, A and B, and produces a Sum and a Carry output. A Half Subtractor subtracts one single-bit binary number B from another A, producing a Difference and a Borrow output. Both circuits are purely combinational and form the basic building blocks of larger arithmetic units such as Full Adders and Full Subtractors.
Boolean Functions
Half Adder:
•	Sum = A ⊕ B
•	Carry = A . B
Half Subtractor:
•	Difference = A ⊕ B
•	Borrow = A' . B

### Files to be Created
File name	Purpose
half_add_sub.v	Arithmetic-circuit RTL
half_add_sub_tb.v	Stimulus and VCD generation

### Verilog Program
// gedit half_add_sub.v
module half_adder (
    input  wire A,
    input  wire B,
    output wire Sum,
    output wire Carry
);
    assign Sum   = A ^ B;   // XOR
    assign Carry = A & B;   // AND
endmodule
 
module half_subtractor (
    input  wire A,
    input  wire B,
    output wire Diff,
    output wire Borrow
);
    assign Diff   = A ^ B;      // XOR
    assign Borrow = (~A) & B;  // A' . B
endmodule

### Testbench Program
// gedit tb3.v
module tb3;
    reg A, B;
    wire Sum, Carry;
    wire Diff, Borrow;
 
    // Instantiate the Half Adder
    half_adder ha_uut (
        .A(A),
        .B(B),
        .Sum(Sum),
        .Carry(Carry)
    );
 
    // Instantiate the Half Subtractor
    half_subtractor hs_uut (
        .A(A),
        .B(B),
        .Diff(Diff),
        .Borrow(Borrow)
    );
 
    initial begin
        // ---- VCD dump setup ----
        $dumpfile("half_add_sub.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb3);                // dump all signals in this testbench hierarchy
 
        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t A=%b B=%b | Sum=%b Carry=%b | Diff=%b Borrow=%b",
                   $time, A, B, Sum, Carry, Diff, Borrow);
        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;
 
        #10 $finish;
    end
endmodule

### Truth Table
<img width="645" height="87" alt="TT3" src="https://github.com/user-attachments/assets/37e33bb3-d647-45d5-b610-c255d7e41b8b" />

### Simulation Procedure

STEP 1 – Open Terminal
Open a terminal in the experiment folder.

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs half_add_sub.v half_add_sub_tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the input combinations and corresponding outputs Sum, Carry, Diff, and Borrow.
A VCD waveform file is also generated:
half_add_sub.vcd

STEP 5 – Open DVE
dve -full64
Other option
dve -full64 &
A DVE environment will open.

DVE Waveform Verification
In DVE:
•	Open the testbench hierarchy.
•	Locate the signals:
o	A
o	B
o	Sum
o	Carry
o	Diff
o	Borrow
•	Add the signals to the waveform window.
•	Run/inspect the waveform.

•	Verify that Sum = 1 whenever A and B are different (A⊕B), and Carry = 1 only when A=1 AND B=1.

•	Verify that Diff = 1 whenever A and B are different (same XOR pattern as Sum), and Borrow = 1 only when A=0 AND B=1.

•	Confirm that Carry and Borrow never both go high for the same input pair, since they represent different (AND vs A'B) conditions.

The waveform should agree with the truth table.

### Expected Result

The Half Adder and Half Subtractor were realized using Verilog HDL:
<img width="600" height="135" alt="exp-3 expected value" src="https://github.com/user-attachments/assets/dcb6103f-1123-4c24-a2fc-203a787744bf" />


The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table
### Output
<img width="1920" height="992" alt="exp-3 wave" src="https://github.com/user-attachments/assets/f00dcdb4-00af-4303-a0b8-56253778c7f5" />


### Result

Thus, the Half Adder and Half Subtractor were designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.





