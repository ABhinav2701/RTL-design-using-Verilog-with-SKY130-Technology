## RTL-design-using-Verilog-with-SKY130-Technology
## Table of contents
* [Day 1: Introduction to iverilog and Yosys](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-1)
   - [Open Source tools for RTL Design and Synthesis](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#11-open-source-tools-for-rtl-design-and-synthesis)
      -  [iverilog](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#i--iverilog)
      -  [GTKWAVE](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#ii-gtkwave)
      -  [YOSYS](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#iii--yosys)
* [Day 2: .libs, hierarchical vs flat synthesis & flop coding](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-2)
* [Day 3:Combinational and sequential optmizations](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-3)










## DAY 3
   ### Combinational and sequential optmizations
   On the third day of workshop emphasis was on logic optimizations on combinational and sequential circuits. Synthesis tools does all the optimization to get most optimised logic using the techniques that is mentioned below.
   ## part 1 
•	Combinational logic optimization
 1) squeezing the logic to get more optimised design
- The most optimised design will be efficient in area and power 
 2) Techniques used for combinational logic optimization
 - a)	Constant propagation:it is a direct optimization technique
    - for example:
    - ![image](https://user-images.githubusercontent.com/88780019/154946214-7a32f9da-4ed3-4167-86d5-f22110d2761c.png)
    - From this we can say that area and power consumption has been reduced by constant propagation technique.
    - Constant ‘0’ on input ‘A’ got propagated down the logic and generated the most optimised logic.
 - b) Boolean logic optimization :it is done using K-map or quine Mckulskey algorithm.
    -![image](https://user-images.githubusercontent.com/88780019/154946492-9c4bbd21-bf02-4892-bd4f-7247a456ec20.png)
    - There is a Boolean logic or k-map reduction is happening in the above
  ###  Sequential logic optimizations
   - a) Sequential constant propagation:
   - for example:
   - ![image](https://user-images.githubusercontent.com/88780019/154946878-e2d229bf-8439-49ae-87c0-9ff1082a70b3.png)
   - Output  ‘Y’ will be always ‘1’ irrespective of Reset and clock pulse.
  ## Lab activity:
   - Combinational logic optimization:
   ![image](https://user-images.githubusercontent.com/88780019/154947060-712fb614-de19-424c-9c5d-b6d9bc892dcb.png)
   -These are the verilog files which has been used for this lab.
   - ![image](https://user-images.githubusercontent.com/88780019/154949196-67a356f8-c754-41c3-b0e7-91ecb2f8c1d7.png)

   - 1) For opt_check module:
      - Expected result:
      - ![image](https://user-images.githubusercontent.com/88780019/154947266-3d836e4b-15b5-4421-bb82-78910ac05af1.png)
      - Lab result:
      - ![image](https://user-images.githubusercontent.com/88780019/154947424-0f5da424-dd1e-41ff-99fb-a842f9ab5f4d.png)
      -  Figure represents netlist of AND gate (expected output).
    -  2) For opt_check2 module:
       - Expected result:
       - ![image](https://user-images.githubusercontent.com/88780019/154947573-5b2c01fe-3aea-48a2-ba0b-6c4bfaf72ff1.png)
       - Lab result:
       - ![image](https://user-images.githubusercontent.com/88780019/154947626-b8b9cfb3-b4b6-4d95-bb9f-9503f85ac8c2.png)
       - Figure represents netlist of OR gate using inverter-inverter followed by a NAND gate.
    - 3) For opt_check3 module:	
        - Expected results:
        - ![image](https://user-images.githubusercontent.com/88780019/154947880-1b43b491-412c-4a9a-a777-bb7b08354106.png)
        - figure represents 3 input NAND gate.
        - Lab result:
        - ![image](https://user-images.githubusercontent.com/88780019/154948179-b3d9b3a3-3d6f-4005-97e1-6fd9a71c001b.png)
        - Figure represents netlist of 3-input AND gate
        
      - Sequential logic optimization:
       - ![image](https://user-images.githubusercontent.com/88780019/154949317-3bc86134-c3b8-4e25-b5b6-c87ee3e06023.png)
       - These are the verilog files which has been used for this lab.
      - a) For dff_const1 module:
       - ![image](https://user-images.githubusercontent.com/88780019/154949679-897ad72e-4d55-4a8b-a819-79778d47335c.png)
       - Expected result:
       - ![image](https://user-images.githubusercontent.com/88780019/154949740-db623e82-8f96-46ef-837b-8ce1401ef53c.png)
       - Lab result:
       - RTL Simulation output:
       - ![image](https://user-images.githubusercontent.com/88780019/154949783-a95f181f-4021-4805-a2da-a371f316333f.png)
       - Synthesis output:
       - ![image](https://user-images.githubusercontent.com/88780019/154949871-a5e30a74-eb32-4a44-95ed-dad1a11eb4e3.png)
       - Figure represents netlist output of dff_const1 module
      - b) For dff_const2 module:
        - ![image](https://user-images.githubusercontent.com/88780019/154950502-692f1227-2e99-4d74-9fc3-6ea10699a894.png)
        - Expected result:
        - RTL simulation result:
        - ![image](https://user-images.githubusercontent.com/88780019/154950574-2a83da0f-1b3c-4a09-8d39-93edd55faf55.png)
        - Synthesis output:
        - ![image](https://user-images.githubusercontent.com/88780019/154950726-8cc6ca43-59c6-45ef-a7f3-bcb5ab9550e9.png)
        -  Figure represents netlist output for dff_const2 (no flip flop present)
       - Sequential optimization of unused outputs:
       - ![image](https://user-images.githubusercontent.com/88780019/154950858-fb37b1ae-44e0-442f-8066-eccee12f76db.png)
       - This is an up counter with output ‘q’ assigned to Lsb of output.
       - Synthesis output:
       - ![image](https://user-images.githubusercontent.com/88780019/154950927-e3d8a994-1dcf-4f68-aa12-f0f76da3e902.png)
     
  ## DAY 4
   ### GLS, blocking vs non-blocking and Synthesis-Simulation mismatch
   - GLS (gate level simulation): running the test bench with netlist as design under test. It verifies logical correctness of the design after synthesis.
      - GLS using iverilog:
      - ![image](https://user-images.githubusercontent.com/88780019/154951986-07649b2d-99df-4ac1-a69d-e7e613f25929.png)
   - Synthesis Simulation Mismatch: It can happen due to certain reasons as mentioned below.
       - a) Missing sensitivity list: When we fail to include all of the variables which directly affect output in the sensitivity list, the output only changes when the variables in the sensitivity list change. This is equivalent to a latch with some enable input, depending on the variables in the sensitivity list. The worse part is that the synthesis tool might not even detect a latch.
       
       ## LAB activity:
       - 1) GLS Synth Sim Mismatch:
       - ![image](https://user-images.githubusercontent.com/88780019/154952324-d5fd389c-854e-4c41-8e85-b1e4ffef7fff.png)
       - RTL simulation output:
       - ![image](https://user-images.githubusercontent.com/88780019/154952478-81724be7-2c58-4735-b0b1-257bccd53c68.png)
       - Synthesis output:
       - ![image](https://user-images.githubusercontent.com/88780019/154952570-8870ca39-4b70-4295-a34a-ea9842888f80.png)
       -  Figure represents netlist of 2*1 mux
       -  GLS using lab(2*1 mux):
       -  RTL simulation output:
       -  ![image](https://user-images.githubusercontent.com/88780019/154952696-9d3566e2-f1f7-45da-a729-e4477de68414.png)
 ## code
 - for generating gate level netlist
 ```
 read_liberty -lib ./my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
 read_verilog ./verilog_files/ternary_operator_mux.v 
 synth -top ternary_operator_mux 
 show
 abc -liberty ./my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
 show
 write_verilog -noattr ternary_mux_netlist.v
 ```
 Synthesis simulation mismatch behaviour using 2*1 mux:
 - ![image](https://user-images.githubusercontent.com/88780019/154954952-f4130e71-1278-4d28-846e-ce5ed6c6175c.png)
 - Rtl simulation for bad_mux
   - ![image](https://user-images.githubusercontent.com/88780019/154955054-94532c86-9927-4ed5-a62a-34b13812e1fd.png)
    - Figure represents like a flop or latch rather than 2*1 mux(mismatch)
 - Synthesis output:
   - ![image](https://user-images.githubusercontent.com/88780019/154955130-e3bfafa0-a22a-4179-85f4-597c368a7b6b.png)
   - Synthesis simulation mismatch due to missing sensitivity list
     - ![image](https://user-images.githubusercontent.com/88780019/154955278-640b67b9-6d36-47ef-b16b-6108eaa6b10b.png)
  
  
  ## DAY 5
   ### optimization in synthesis
   - If case constructs:
   - a) If statements:it is used only for priority logic.
   - for example:
   - ![image](https://user-images.githubusercontent.com/88780019/154956076-74338e0b-533e-4086-8bca-ae8130015982.png)
   - Danger/caution with if statement: it causes ‘inferred latches’.it is because of bad coding style that comes due to incomplete if statements.
   - ![image](https://user-images.githubusercontent.com/88780019/154956222-e555755e-d1ad-4a85-915a-ab3491b435c1.png)
   - Figure represents inferred latch because of incomplete if statement.


   - b) CASE statement:
   ```
   case ()
      case_item1:
case_item2,
     case_item3:
     case_item4:
     begin

end
      default:
 endcase
   ```
NOTE:  if ‘case statement’ is incomplete then it will also results into inferred latches as previously. To avoid this we should write code ‘case with default’.
  - LAB activity:
  - a) Incomplete if :
    - ![image](https://user-images.githubusercontent.com/88780019/154956630-73990ade-8328-4f5e-a423-a7d489f7e37f.png)
  - RTL simulation output:
    - ![image](https://user-images.githubusercontent.com/88780019/154956704-f73707ea-d4b0-4404-825f-70ad2e5efe72.png)
    - figure represents D flip flop.
  - Synthesis output:
    - ![image](https://user-images.githubusercontent.com/88780019/154956796-752a0acf-aba4-4858-99be-6477178fad34.png)
    - ![image](https://user-images.githubusercontent.com/88780019/154956822-e763b634-5ee6-4439-bb5e-f98732620850.png)

  - b) Incomplete if2:
    - ![image](https://user-images.githubusercontent.com/88780019/154956945-baeebd30-5300-403e-ba63-97f919a02175.png)
    - RTL simulation output:
      - ![image](https://user-images.githubusercontent.com/88780019/154956997-95b45ad6-eac8-4ed9-88e6-b27e00031fe3.png)
    - Synthesis output:
      - ![image](https://user-images.githubusercontent.com/88780019/154957037-b1923ca0-770b-4369-87bf-6abfa85225a8.png)
 
 - c) Case statement:
    - a)	Incomplete case
    - ![image](https://user-images.githubusercontent.com/88780019/154958383-6185b241-d200-4800-96d9-3364d29b5fd3.png)
    - RTL simulation output:
      - ![image](https://user-images.githubusercontent.com/88780019/154958422-3200bdb4-ffaf-438d-9c6d-d190a6c1a266.png)
    - Synthesis output:
      - ![image](https://user-images.githubusercontent.com/88780019/154958516-9a841c13-fb75-412f-a4b4-efd028254d0d.png)
    - b) Complete case:
    - ![image](https://user-images.githubusercontent.com/88780019/154958599-82a8d544-bb51-46c4-947c-5c2d601da791.png)
     - RTL simulation output:
       - ![image](https://user-images.githubusercontent.com/88780019/154958677-903cab5a-2465-4d01-a285-db7653239892.png)
     -  synthesis output:
        - ![image](https://user-images.githubusercontent.com/88780019/154958749-15376efa-52b9-43e4-b8b0-b26f430f9edd.png)
    - c) Partial case:
    -  ![image](https://user-images.githubusercontent.com/88780019/154959000-896034db-d9f2-4df1-ae9c-8d0d163de68f.png)
    -  Synthesis output:
       - ![image](https://user-images.githubusercontent.com/88780019/154959071-3a88c484-f627-4474-9153-7676f50c55b3.png)

    - d) Bad case:
    - ![image](https://user-images.githubusercontent.com/88780019/154959203-adbf7af4-2040-4307-a7c4-23f6a9021024.png)
    - RTL simulation output:
      - ![image](https://user-images.githubusercontent.com/88780019/154959256-286df982-0638-49a0-bb19-446b7986ad8e.png)
    - synthesis output:
      - ![image](https://user-images.githubusercontent.com/88780019/154959319-b80562df-0385-476b-9bd9-47dd5adfa094.png)
    - GLS simulation output:
    - ![image](https://user-images.githubusercontent.com/88780019/154959393-5173a430-562a-4866-bea4-6bd56c565218.png)
  
  
# LOOPING CONSTRUCTS
  - a) FOR LOOP:  It is used inside ‘always’ block.it is used for evaluating expressions.
  -  b) GENERATE-FOR LOOP: It is never used inside ‘always’ block.it is used for instantiating hardware.
 
 - LAB activity:
    - a)	Mux generator:
       - ![image](https://user-images.githubusercontent.com/88780019/154961299-8a9693c0-8e89-45a2-a42d-3b2aabb28ee0.png)
     - RTL simulation output:
        - ![image](https://user-images.githubusercontent.com/88780019/154961430-4b5f2df3-627e-4ba4-8642-ec0edde61e79.png)
     -  Synthesis output:
        - ![image](https://user-images.githubusercontent.com/88780019/154961583-ded4dc3c-221f-46fe-8906-58e572fbed2c.png)
     - b)	Demux case:
        - ![image](https://user-images.githubusercontent.com/88780019/154961700-095ef9ef-d553-460c-80c7-730f4aaa432d.png)
      - RTL simulation output:
        - ![image](https://user-images.githubusercontent.com/88780019/154961787-dc37810b-584c-4f81-81d6-6cb978796221.png)
      - c) Demux generate:
        - ![image](https://user-images.githubusercontent.com/88780019/154962434-8e9603a2-d7bb-46be-a2e9-5f64419df0c3.png)
       - RTL simulation output:
         - ![image](https://user-images.githubusercontent.com/88780019/154962505-74a238cf-08a2-4169-9ac4-e9b9e03c0668.png)
      - d)	Generate for loop(Ripple carry adder):
        - ![image](https://user-images.githubusercontent.com/88780019/154962593-acda4aff-95bf-4e38-a3c8-d096255e896b.png)
       - RTL simulation:
         - ![image](https://user-images.githubusercontent.com/88780019/154962637-77a612a7-d073-49ba-8e45-3bf77b0610f9.png)
       
 


  
 
 
 
 
  
    -  
   

    - 
   


   

   

      



 







       
 







      
       - 


    








    
