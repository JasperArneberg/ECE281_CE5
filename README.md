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
###Signal Descriptions

###Waveform
![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/screenshot.png?raw=true "Screenshot")

#Task 3
###Waveform
![alt text](https://github.com/JasperArneberg/ECE281_CE5/blob/master/screenshot.png?raw=true "Screenshot")

#Demonstrations
| Functionality | Witness | Date | Time |
| :--: | :--: | :--: | :----: |
| Task 1 | | | |
| Task 2 | | | |
| Task 3 | | | |

#Documentation
None as of now.
