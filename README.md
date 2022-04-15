# Lab7

//PC

module PC(reset, clock, PC2, PC1);

input reset, clock; 

input [7:0] PC2;

output reg [7:0] PC1;


always @(*) begin

if (reset)

PC1 = 8'd0;

else

PC1 = PC2;

end

endmodule 


//Adder+4

module Adder( PC1, PC2);

input [7:0] PC1;

output  [7:0] PC2;


assign PC2 = PC1 + 8'd4;


endmodule 

//ROM

module ROM(address, out);

input [7:0] address;

output [31:0] out;

reg [31:0] result;

assign out = result;

always @(address) begin

case (address)

8'd00: result = 32'h00000000;

8'd04: result = 32'h00100713;

8'd08: result = 32'h00b76463;

8'd12: result = 32'h00008067;

8'd16: result = 32'h006a803;

8'd20: result = 32'h00068613;

8'd24: result = 32'h00070793;

8'd28: result = 32'hffc62883;

8'd32: result = 32'h01185a63;

8'd36: result = 32'h01162023;

8'd40: result = 32'hfff78793;

8'd44: result = 32'hffc60613;

8'd48: result = 32'hfe0796e3;

8'd52: result = 32'h00279793;

8'd56: result = 32'h00f507b3;

8'd60: result = 32'h0107a023;

8'd64: result = 32'h00170713;

8'd68: result = 32'h00468693;

8'd72: result = 32'hfc1ff06f;

endcase

end

endmodule 


//Instruction Decoder

module InstrDecoder(Is, rd, rs1, rs2, imm);

output [4:0] rd, rs1, rs2;

output [11:0] imm;

input[31:0]Is;

assign rd = Is[11:7];

assign rs1 = Is[19:15];

assign rs2 = Is[24:20];

assign imm = Is[31:20];


/*always @(*)

begin

end*/

endmodule 

//Top Level File 


module ProgramCounter(rst, clk, out1, out2, out3, out4, out5);

wire [7:0] in0, out0;

input clk, rst;

output [31:0] out1;

output [4:0] out2, out3, out4;

output [11:0] out5;

PC pc0(rst, clk, in0, out0); 

Adder adder0(out0, in0);

ROM rom0(out0, out1);

InstrDecoder decoder0(out1, out2, out3, out4, out5);

always @(*)

begin

end

endmodule
