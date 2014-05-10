ECE281_CE5
==========

ECE 281 Computer Exercise 5: MIPS

C3C Jasper Arneberg  
M6A ECE 281  
Dr. Neebel  


#Task 1

Initialize registers $S0 and $S1 with the decimal values 44 and -37 respectively. Use register instruction to add these values and store the result in $S2. Finally store the value in $S2 to the address x54.

```
I-type 0x2010002C addi $S0, $zero, 44
R-type 0x02F34022 sub $t0, $S7, $S3

High level code:
b = 44; //$S1
c = -37; //$S2
a = b + c; //$S0
//Store a to address


MIPS Assembly Code:
# $S0 = a, $S1 = b, $S2 = c
  addi $S1, $0, 0x002c # b = 44
  addi $S2, $0, 0xffdb # c = -37
  add $S0, $S1, $S2 # a = b + c
  sw $S0, 0x54 # write a to address x54
```


#Task 2
Hand-assemble the program from Task 1.
```
MIPS Assembly Code:                             Machine Language:
  addi $S1, $0, 0x002c # b = 44                   0x2011002c
  addi $S2, $0, 0xffdb # c = -37                  0x2012ffdb
  add $S0, $S1, $S2 # a = b + c                   0x02328020
  sw $S0, 0x54 # write a to address x54           0xac100054
```


###Signal Descriptions

This program appears to have worked as planned. As can be seen in the waveform below, the value of 7 is being written ot he x54 address. The value 7 is in the writedata signal, and the aluout signal has a value of x54.

###Waveform
![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/task1screenshot.png?raw=true "Task 2 Screenshot")

#Task 3

### Modifications
The datapath schematic was drawn for the ori command. No physical changes were necessary because the ALU is capable of performing or instructions.

![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/datapath_schematic.jpg?raw=true "Datapath Schematic")

The ALU decoder was changed so that it would execute the ori command. Here is the table with the summary of changes.

![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/alu_decoder.jpg?raw=true "ALU decoder")

The control signals were set for an ori command:
```
when "001101" => controls <= "101000010"; -- ori
```

Below is the modification to extend the functionality of the ALU decoder:
```
when "11" => alucontrol <= "001"; -- or
```

### Testbench
A new instruction was added to the testbench to see if the ori command would execute as expected.

```
MIPS Assembly Code:                             Machine Language:
  addi $S1, $0, 0x002c # b = 44                   0x2011002c
  addi $S2, $0, 0xffdb # c = -37                  0x2012ffdb
  add $S0, $S1, $S2 # a = b + c                   0x02328020
  sw $S0, 0x54 # write a to address x54           0xac100054
  ori $S3, $S2, x80000                            0x36538000
```

The hand compilations can all be seen below in this photograph:
![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/hand_compilation.jpg?raw=true "Hand Compilation")

###Waveform Analysis
![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/task3waveform.png?raw=true "Task 3 Waveform")

The ori operation appears to have worked. This operation compares the value of $S2, which was 0xffffffdb from before, and it compares it with the immediate value of 0x000080000. The expected result of an or operation would be 0xffffffdb, which is exactly what we see in the aluout signal after 50 ns.

#Documentation
I got ideas for how to solve task 3 from Hamza El-Saawy, Brian Yarbrough, and Daniel Eichman.
