EXP-2

Date:

                  SIMULATION AND IMPLEMENTATION OF COMBINATIONAL LOGIC CIRCUITS

AIM:

 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.2

APPARATUS REQUIRED: 

VIVADO 2023.2

PROCEDURE:

STEP:1 Launch the Vivado 2023.2 software.

STEP:2 Click on “create project ” from the starting page of vivado.

STEP:3 Choose the design entry method:RTL(verilog/VHDL).

STEP:4 Crete design source and give name to it and click finish.

STEP:5 Write the verilog code and check the syntax.

STEP:6 Click “run simulation” in the navigator window and click “Run behavioral simulation”.

STEP:7 Verify the output in the simulation window.

LOGIC DIAGRAM

ENCODER

![328582891-efe2b90d-7a2e-48b0-9dea-021660cbb2e0](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/a4c2fe52-0bdc-4e2b-b429-30c06d4ab85e)



verilog code
```
module encoder(a,y);
input [7:0]a;
output[2:0]y;
or(y[2],a[6],a[5],a[4],a[3]);
or(y[1],a[6],a[5],a[2],a[1]);
or(y[0],a[6],a[4],a[2],a[0]);
endmodule
```
output

![328583339-0a7dae4d-195d-4478-ab95-7fa72bff1cb0](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/a09c0e81-b8fb-4c24-883a-c46ac6fd4998)



LOGIC DIAGRAM DECODER

![328583716-379dfab4-6571-4e74-b3f0-7fad4010dcb4](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/a7faf161-6a01-4f9b-a32d-578d1307d2b1)


verilog code
```
module decoder1(a,y);
input [2:0]a;
output[7:0]y;
and(y[0],~a[2],~a[1],~a[0]);
and(y[1],~a[2],~a[1],a[0]);
and(y[2],~a[2],a[1],~a[0]);
and(y[3],~a[2],a[1],a[0]);
and(y[4],a[2],~a[1],~a[0]);
and(y[5],a[2],~a[1],a[0]);
and(y[6],a[2],a[1],~a[0]);
and(y[7],a[2],a[1],a[0]);
endmodule
```
output

![328584252-21cc150c-9fc2-4b5a-b779-b3a6b1e57e98](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/714a9ab3-1743-44f2-b514-e0c7d717a3a2)


LOGIC DIAGRAM MULTIPLEXER

![328585145-cd7ef931-2f82-44dc-8110-321214476a4f](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/0f167682-8652-4924-ab99-c8a102da91b7)



VERILOG CODE
```
module mux(s,c,a);
input [2:0]s;
input [7:0]a;
wire [7:0]w;
output c;
and(w[0],a[0],~s[2],~s[1],~s[0]);
and(w[1],a[1],~s[2],~s[1],s[0]);
and(w[2],a[2],~s[2],s[1],~s[0]);
and(w[3],a[3],~s[2],s[1],s[0]);
and(w[4],a[4],s[2],~s[1],~s[0]);
and(w[5],a[5],s[2],~s[1],s[0]);
and(w[6],a[6],s[2],s[1],~s[0]);
and(w[7],a[7],s[2],s[1],s[0]);
or (c,w[0],w[1],w[2],w[3],w[4],w[5],w[6],w[7]);
endmodule
```
output

![328585663-8dd1c71b-e233-4725-96d7-70477fa1babd](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/353bfdfb-d324-4001-88b3-62a209d0ad82)


VERILOG CODE DEMULTIPLEXER

![328586052-7499dabf-d2bd-48b0-88ec-fd33fc3bf323](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/fcd22d04-7fd7-4eed-b52e-d95dda928859)



VERILOG CODE
```
module demux_8(s,a,y);
input [2:0]s;
input a;
output [7:0]y;
and(y[0],a,~s[2],~s[1],~s[0]);
and(y[1],a,~s[2],~s[1],s[0]);
and(y[2],a,~s[2],s[1],~s[0]);
and(y[3],a,~s[2],s[1],s[0]);
and(y[4],a,s[2],~s[1],~s[0]);
and(y[5],a,s[2],~s[1],s[0]);
and(y[6],a,s[2],s[1],~s[0]);
and(y[7],a,s[2],s[1],s[0]);
endmodule
```

output

![328586729-31b3314b-b860-40ff-9334-b0ee03ed5a5f](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/34d8a62b-d1c3-4189-ae99-61fdd1dfc626)


MAGNITUDE COMPARATOR

![328587068-438bf227-3184-4629-9e37-92c0ee354a9b](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/dce862e5-1f4d-4b87-862f-c84cc067275f)


VERILOG CODE
```
module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
 if (a==b)
 begin
  eq = 1'b1;
  lt = 1'b0;
  gt = 1'b0;
 end
 else if (a>b)
 begin
  eq = 1'b0;
  lt = 1'b0;
  gt = 1'b1;
 end
 else
 begin
  eq = 1'b0;
  lt = 1'b1;
  gt = 1'b0;
 end
end 
endmodule
```
OUTPUT

![328588837-08d2e7c6-2608-4faf-8d17-a85311763ce5](https://github.com/Naradinakar/VLSI-LAB-EXP-2/assets/161109578/8191bde6-5b64-4926-9028-b186ab533b56)


RESULT:

Thus the simulation and synthesis of ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, 2bit MAGNITUDE COMPARATOR using vivado is successfully completed and executed.



