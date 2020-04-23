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
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/01.png)

## Running the strings command to get all the strings in the binary

 Finding strings in binary

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/02.png)
 
 ### On the basis of the result we try different input this time to the binary 
 
 Passing "vacanteee" as input to the binary and observing the result

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/03.png)
 
 it can be observed that we get different output this time , but not so useful .
 
## Using gdb-peda to analyze the binary 
This process will help us see the value of all the registers that what address are there in each registers and if it is readable .

```
Using gdb-peda to see the registers by setting breakpoint on the main function and running the function . 
\# file is used to tell gdb-peda to which file to run``` 
file casino  
\# break to set the breakpoint on the function so that execution stops here 
break *main
\# run to start the program and strop when the break point is reached 
run
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/04.png)

Continue the program and input a string .

```
\# c to continue the program 
c
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/05.png)

Try to get the segmentation error , to exploit we need to identiy the segmentation error . Inorder to get the segmentation error we need to submit a long string so that we overflow the buffer .

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/06.png)

Here we can see that we have overflown the EIP register . And overwritten the reqister with A's

Create the pattern and find the offset for the EIP register 
```
\# pattern-create creates a long payload with the length defined by the user it helps to find the offset   
pattern create 200
run
c
\# Enter the text which we got from the create-pattern 
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/07.png)

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/08.png)

It can be observed that the EIP register is overflown and the text is **AACG** .

To get the offset using the string in the EIP register 
```
\# patts to get the offset for the registers 
patts
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/09.png)

Now we know that that after 55 letters whatever we enter goes in EIP register so now we can give instruction to the register . So finally we control are able to control the EIP register .

### Now we need to give a memory address of the instruction which we want to execute .

Exploring the executable using radare2 which is an open source dissassembler and debugger .

```
\# To load the executable in the tool
radare2 casino
\# To start analysis
aaa
\# To list all the functions 
afl
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/10.png)

**sym.win** is an interesting function . To dissasmble and see the assemble code . 
```
s sym.win
pdf
```
![](https://github.com/ashu1665/BufferOverflow/blob/master/action/11.png)

So now we are in the sym.win function we can see the working of the function so here it takes argument and compares with some value and we can see it's true it jumps some where and prints **You_are_not_1337_enough** . So in order to go to the other path we have to make the cmp() to return true .

So to do that we create a payload with the address of the sym.win function and the correct argument value of for the fuction and the return address which we can get using the ropper command . 

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/12.png)

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/13.png)

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/14.png)

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/15.png)

![](https://github.com/ashu1665/BufferOverflow/blob/master/action/16.png)





 



