## RTL-design-using-Verilog-with-SKY130-Technology
![image](https://user-images.githubusercontent.com/88780019/154992867-a94d73a1-3f4d-41cb-ab83-152bacd7a91f.png)

## Table of contents
* [Day 1: Introduction to iverilog and Yosys](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-1)
   - [Open Source tools for RTL Design and Synthesis](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#11-open-source-tools-for-rtl-design-and-synthesis)
    1. [iverilog](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#i--iverilog)
    2. [GTKWAVE](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#ii-gtkwave)
    3. [YOSYS](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#iii--yosys)
* [Day 2: .libs, hierarchical vs flat synthesis & flop coding](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-2)
    1. [Introduction to .lib](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-introduction-to-lib)
    2. [Heirarchial vs flat synthesis](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-heirarchial-vs-flat-synthesis)
    3. [ Flop coding style](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-flop-coding-style)
* [Day 3:Combinational and sequential optmizations](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-3)
   1. [Combinational logic optimization](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-Combinational-logic-optimization)
	2. [Sequential logic optimizations](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#32-Sequential-logic-optimizations)
	3. [ Lab activity:](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-Lab-activity-:)  
* [Day 4:GLS, blocking vs non-blocking and Synthesis-Simulation mismatch](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-4)
   1. [ GLS (gate level simulation):](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-GLS-(-gate-level-simulation-)-:)
	2. [ Lab activity:](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-Lab-activity-:) 
* [Day 5:optimization in synthesis](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#day-5)
   1. [If statements:](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-If-statements-:) 
	2. [CASE statement:](https://github.com/ABhinav2701RTL-design-using-Verilog-with-SKY130-Technology#-CASE-statement-:)
	3. [ Lab activity:](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-Lab-activity-:)  
	4. [LOOPING CONSTRUCTS](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#-LOOPING-CONSTRUCTS)
* [Credits](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#credits)
* [References](https://github.com/ABhinav2701/RTL-design-using-Verilog-with-SKY130-Technology#references)





## DAY 1
 ### Introduction to iverilog and Yosys
 - RTL design:it is set of Verilog code which has intended functionality to meet with the required specification.
 - Iverilog simulator flow:
    -![image](https://user-images.githubusercontent.com/88780019/154971298-b6f5dd2d-2e04-46ba-9232-e130a0d7e9d3.png)
    
 - LAB activity:
   - Git cloning from repositories(sky130RTLDesignAndSynthesisWorkshop)
 - code 
   ```
   https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
   ```
   - verilog files that are used for the workshop:
   - ![image](https://user-images.githubusercontent.com/88780019/154972400-9403231c-2d2e-4d31-b300-c07aa70eaf33.png)
   - iverilog(simulation of 2*1 mux):
     - ![image](https://user-images.githubusercontent.com/88780019/154989637-cbe1a672-7a20-4390-90a5-4e8a155a2570.png)
     - ![image](https://user-images.githubusercontent.com/88780019/154989654-9f71cd12-98d6-4bf6-b951-ee16eda0f5eb.png)
    -RTL simulation output:
        - ![image](https://user-images.githubusercontent.com/88780019/154989743-485533d3-29dd-4aee-b123-da401dfae6c1.png)
     
     
  - yosys: : Yosys is an open source RTL synthesis tool which takes verilog file of a design and technology library file(.lib) as inputs and generates gate level netlist corresponding the functional behaviour of the design.
     - ![image](https://user-images.githubusercontent.com/88780019/154992236-5cd370a8-3aad-40ba-82cd-48b92dbbbc2d.png)
     -![image](https://user-images.githubusercontent.com/88780019/154990136-58d121c2-3998-444c-b322-22565a3d5f66.png)
  # code for synthesis(gererating a netlist)
  ```
  yosys
  
  read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog good_mux.v
  
  synth -top good_mux
  
  abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
  
 synthesis output:
   - ![image](https://user-images.githubusercontent.com/88780019/154990854-43fabf37-1ad2-4dd3-9bf0-87deac33564d.png)
   - figure represents the netlist of 2*1 mux
  # code
  ```
  write_verilog good_mux_netlist.v

  !gvim good_mux_netlist.v
  ```
  output:
  - ![image](https://user-images.githubusercontent.com/88780019/154991839-f80a6b75-4f2d-494d-91a6-9077e73e1482.png)

## DAY 2 
  ###  Introduction to .lib, Heirarchial vs flat synthesis and Flop coding style
  
   ### ** Introduction to .lib**
   1) understanding the .lib file
        - ![image](https://user-images.githubusercontent.com/88780019/154995061-c5e8b104-cc2a-42ae-8aeb-95da200f260d.png)
   # code
   ```
   gvim ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   
   
   -![image](https://user-images.githubusercontent.com/88780019/154995758-2d226e9a-c91f-4366-83cc-e0583c34083f.png)
   - the information of Timing, power area and other details of standard cell AND gate of .lib file.
       
       
   # Hierarchical and Flat synthesis
       
   # LAB activity
    Hierarchial Synthesis
    - code
    ```
    gvim multiple_modules.v
    ```
 verilog code:
 - ![image](https://user-images.githubusercontent.com/88780019/154999160-49f0424a-4399-4ad0-93ed-b6d3932acf76.png)

# code for synthesis
```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
write_verilog -noattr multiple_modules_hier.v
!gvim multiple_modules hier.v

```

Synthesis output:
  - ![image](https://user-images.githubusercontent.com/88780019/154999767-d81ee0b3-2147-4295-9625-9458636218fe.png)
  - ![image](https://user-images.githubusercontent.com/88780019/155000274-a2c5ffd2-b1a3-4f51-84d5-29386155352a.png)
  - ![image](https://user-images.githubusercontent.com/88780019/155000858-95145d9b-bcd3-41e0-a5c5-cae150bdb774.png)
  - The submodules are preserved and they don't get flattened to gates by default, leading to hierarchical nature of the modules.
 
 - NOTE: we can use flatten in the prompt to eliminate the hierarchies leading to flat synthesis.
  
  # code
  ```
  flatten
  
  write_verilog -noattr multiple_modules_flat.v
  
  !gvim multiple_modules hier.v
  ```
   output:
     - ![image](https://user-images.githubusercontent.com/88780019/155002015-1842ab8e-68d3-4352-9846-5d220171ceea.png)
     - ![image](https://user-images.githubusercontent.com/88780019/155002548-b1c58a76-c349-4377-a2d5-562f7a3211ff.png)
     - figure represents gate-level netlist of the flattened module.
   
   - submodule level synthesis:
     # code
      ```
      yosys
      read_verilog multiple_modules
      synth -top sub_module1
      abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
      show
      ```
  output:
  - ![image](https://user-images.githubusercontent.com/88780019/155003308-a1379855-c515-4278-8a72-440c724019ee.png)
  - ![image](https://user-images.githubusercontent.com/88780019/155003409-340e5be2-aed5-4510-bbfb-7b479b601b73.png)
 
   NOTE:when there are multiple instances of same module. It's convenient to synthesize a module once and replicate it wherever the module is needed instead of directly     synthesizing every instance of that module. In a massive design, a synthesizer might fail to synthesize desirably and so synthesizing lower level modules first and then proceeding with the top-level module will let the synthesizer produce the desired netlist.
 
  # flop coding style
  
   - Flops are introduced between the combinational circuits to avoid glitches in the circuit.

  # Lab activity:
  these are the verilog files which is used for this lab.
  - ![image](https://user-images.githubusercontent.com/88780019/155004969-503df9b7-c41f-465b-910a-a580b2375b48.png)

    - 1) Flop with asynchronous reset
      - ![image](https://user-images.githubusercontent.com/88780019/155004646-1bef920d-287a-4124-b80f-2e7cad6afcbe.png)
  # code
  ```
  ls *dff*
  iverilog dff_asyncres.v tb_dff_asyncres.v
  ./a.out
  gtkwave tb_dff_asyncres.vcd
  ```
 RTL simulation output:
  - ![image](https://user-images.githubusercontent.com/88780019/155005546-95799140-7cdd-4d91-b236-e2032e5330e2.png)
  
  - synthesis output:
    - ![image](https://user-images.githubusercontent.com/88780019/155008413-240bb7bf-706c-4300-b81f-6ec557c35afe.png)


     - 2) Flop with asynchronous set
       - ![image](https://user-images.githubusercontent.com/88780019/155005920-74497c02-7620-4cd0-8884-b9ae585de67f.png)
     # code
     ```
     iverilog dff_async_set.v tb_dff_async_set.v
     ./a.out
     gtkwave tb_dff_async_set.vcd
     ```
  RTL simulation output:
    - ![image](https://user-images.githubusercontent.com/88780019/155006319-569ab511-2a0d-4c5b-9ac3-11ff7999df0f.png)
    
   - Synthesis output:
      - ![image](https://user-images.githubusercontent.com/88780019/155008667-9383b388-acc8-4fc4-a35d-32aeca5d44be.png)

    
    
    
     - 3) Flop with synchronous reset
         - ![image](https://user-images.githubusercontent.com/88780019/155006565-1caf09c5-db6e-4580-975a-bba605fe8e50.png)
   
   
   # code
   ```
    iverilog dff_syncres.v tb_dff_syncres.v
    ./a.out
    gtkwave tb_dff_syncres.vcd
    
   ```
    
 RTL simultation output:
    - ![image](https://user-images.githubusercontent.com/88780019/155007609-7f0abb00-f262-4dbf-a300-0720cd297648.png)
        
 - Synthesis output:
   -![image](https://user-images.githubusercontent.com/88780019/155008930-97eaf7ba-469f-4726-8ae1-b7d77e45beef.png)
 

## DAY 3
   ### Combinational and sequential optmizations
   On the third day of workshop emphasis was on logic optimizations on combinational and sequential circuits. Synthesis tools does all the optimization to get most optimised logic using the techniques that is mentioned below. 
 ## Combinational logic optimization
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
   # GLS (gate level simulation): 
      -running the test bench with netlist as design under test. It verifies logical correctness of the design after synthesis.
      - GLS using iverilog:
      - ![image](https://user-images.githubusercontent.com/88780019/154951986-07649b2d-99df-4ac1-a69d-e7e613f25929.png)
   - Synthesis Simulation Mismatch: It can happen due to certain reasons as mentioned below.
        - a) Missing sensitivity list
        - b) Blocking vs non-blocking assignments
        - c) Non-standard Verilog coding

       
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
   # If statements:
   - it is used only for priority logic.
   - for example:
   - ![image](https://user-images.githubusercontent.com/88780019/154956076-74338e0b-533e-4086-8bca-ae8130015982.png)
   - Danger/caution with if statement: it causes ‘inferred latches’.it is because of bad coding style that comes due to incomplete if statements.
   - ![image](https://user-images.githubusercontent.com/88780019/154956222-e555755e-d1ad-4a85-915a-ab3491b435c1.png)
   - Figure represents inferred latch because of incomplete if statement.


   # CASE statement:
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
  # LAB activity:
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

 
## Credits
 1. [Kunalg github profile](https://github.com/kunalg123)

## References
  1. [Yosys Docs](http://yosyshq.net/yosys/documentation.html)
  2. [nandland](https://www.nandland.com/)
  3. [vsdiat](http://vsdiat.com/)
  4. [VLSI System Design](https://www.vlsisystemdesign.com/)

 


  
 
 
 
 
  
    -  
   

    - 
   


   

   

      



 







       
 







      
       - 


    








    
