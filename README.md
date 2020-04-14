# BufferOverflow
This is the description of how i exploited a bufferoverflow on a binary using function argument .

## Basics that is required for the exploitation

1.x86 architecture

2.Physical memory in the x86 architecture

3.Stack memory

4.Function return mechanism

5.Resgisters mainly EIP

## Goal when trying to exploit bufferoverflow

## Starting to explore the binary file given for the task

 Running the binary
01

## Running the strings command to get all the strings in the binary

 Finding strings in binary
02
 
 
 ### On the basis of the result we try different input this time to the binary 
 
 Passing "vacanteee" as input to the binary and observing the result
03
 
 it can be observed that we get different output this time , but not so useful .
 
## Using gdb-peda to analyze the binary 

Using gdb-peda to see the registers by setting breakpoint on the main function and running the function . 

04


 



