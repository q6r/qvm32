qvm32
=====

This is a very basic and badly written crackme running in a virtual machine that follows a simple design.
Four general registers r[1-4], rs, ri. A stack, no heap. A list of instructions:
```
RET   = 0x11, // opcode
CALL  = 0x22, // opcode
MOV   = 0x33, // mov reg, reg|imm
PUSH  = 0x44, // push reg|imm
ECALL = 0x55, // ecall imm
CMP   = 0x66, // cmp reg, reg|imm
JMP   = 0x77, // jmp imm
JZ    = 0x88, // jz imm
JNZ   = 0x99, // jnz imm
MOVP  = 0xaa, // movp reg, imm
AND   = 0xbb, // and reg, reg|imm
ADD   = 0xcc, // add reg, reg|imm
XORP  = 0xdd  // xorp reg, reg|imm
```
badly implemented :) this was written in a very short time for a crackme challenge many of the instructions were
not implemented well or used by the byte codes interrupted in the application. Anyway, have fun. The byte code of
the crackme translates to something like

```
// Get user input
write(0x01, "ENTER PASS :", 0x0c);
read(0x00, 0x000000f2, 0x0c);
 
//XOR input with our xor key
MOV [IMM] r1 0x000000f2
XOR [IMM] r1 0x13
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0x37
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xd3
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0x3d
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xc0
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xde
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xab
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xad
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0x1d
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0xea
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0x13
ADD [IMM] r1 0x00000001
XOR [IMM] r1 0x37
ADD [IMM] r1 0x00000001
 
// Do Comparisions
MOVP r1, 0x000000f2
MOV r2, 0x000000..
MOVP r3, 0x000000f3
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
MOVP r1, 0x000000f4
MOV r2, 0x000000..
MOVP r3, 0x000000f5
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
MOVP r1, 0x000000f6
MOV r2, 0x000000..
MOVP r3, 0x000000f7
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
MOVP r1, 0x000000f8
MOV r2, 0x000000..
MOVP r3, 0x000000f9
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
MOVP r1, 0x000000fa
MOV r2, 0x000000..
MOVP r3, 0x000000fb
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
MOVP r1, 0x000000fc
MOV r2, 0x000000..
MOVP r3, 0x000000fd
MOV r4, 0x000000..
CMP r1, r2
JNZ failed
CMP r3, r4
JNZ failed
 
// Win if not failed and exit
write(0x01, "WIN\n", 0x4)
EXIT(ff);
write(0x01, "FAILED\n", 0x0c);
```
This is simple takes user input xor each byte with a key and then compares each byte
with values if any is wrong then it exist. This can be solved in various ways.
1) Password can be predicted if wrong or right by counting executed instructions if more 
executed then it's correct if less then it's wrong..etc PIN dynamic binary instrumental tool
can help in this process.
2) by understanding the VM and then understanding the crackme
3) be creative!

Password is : iWasteMyTime
http://0x80.org/blog/qvm32-solution-and-virtualization-obfuscation/