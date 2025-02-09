# GDB Cheat Sheet

```jsx
By: n0tabdu11ah
```

### **Starting & Attaching**

|Command|Description|Example|
|---|---|---|
|`gdb <binary>`|Load a binary into GDB|`gdb ./a.out`|
|`gdb -p <pid>`|Attach to a running process|`gdb -p 1337`|
|`attach <pid>`|Attach to an existing process|`attach 5678`|
|`detach`|Detach from the process|`detach`|
|`info inferiors`|List attached processes|`info inferiors`|

---

### **Execution Control**

|Command|Description|Example|
|---|---|---|
|`run <args>`|Start program with arguments|`run input.txt`|
|`start`|Start program and stop at `main()`|`start`|
|`continue` (or `c`)|Continue execution|`continue`|
|`next` (or `n`)|Step over next line (C level)|`next`|
|`step` (or `s`)|Step into next line|`step`|
|`finish`|Run until function returns|`finish`|
|`si`|Step into next **instruction** (assembly)|`si`|
|`ni`|Step over next instruction|`ni`|
|`jump *<addr>`|Jump execution to an address|`jump *0x4005d4`|

---

### **Memory Inspection & Modification**

|Command|Description|Example|
|---|---|---|
|`x/<n><fmt> <addr>`|Examine memory at address|`x/10x 0x601040`|
|`x/s <addr>`|Print string at address|`x/s $rsp`|
|`x/i <addr>`|Show instruction at address|`x/i $rip`|
|`info proc mappings`|Show memory layout|`info proc mappings`|
|`set *(int*)<addr> = <val>`|Modify memory value|`set *(int*)0x601040 = 0x1337`|

Formats for `x` command:

- `x` → hex
- `d` → decimal
- `s` → string
- `i` → instruction
- `b`/`h`/`w`/`g` → 1, 2, 4, 8-byte chunks

---

### **Disassembly & Code Analysis**

|Command|Description|Example|
|---|---|---|
|`disas <func>`|Disassemble function|`disas main`|
|`disas /r <func>`|Show raw opcodes|`disas /r main`|
|`si`|Step one instruction|`si`|
|`ni`|Step over one instruction|`ni`|
|`layout asm`|View assembly window|`layout asm`|

---

### **Breakpoints & Watchpoints**

|Command|Description|Example|
|---|---|---|
|`b <func>`|Break at function|`b main`|
|`b *<addr>`|Break at address|`b *0x4005d4`|
|`b <file>:<line>`|Break at file:line|`b exploit.c:42`|
|`tbreak <func>`|Temporary breakpoint|`tbreak main`|
|`watch <var>`|Stop on variable change|`watch counter`|
|`rwatch <var>`|Stop on variable read|`rwatch buffer`|
|`awatch <var>`|Stop on read/write|`awatch array[0]`|
|`info breakpoints`|Show breakpoints|`info breakpoints`|
|`delete <num>`|Remove breakpoint|`delete 1`|

---

### **Registers & Stack**

|Command|Description|Example|
|---|---|---|
|`info registers`|Show all registers|`info registers`|
|`i r <reg>`|Show specific register|`i r eax`|
|`set $<reg> = <val>`|Modify register value|`set $eax = 0xdeadbeef`|
|`info frame`|Get stack frame info|`info frame`|
|`info stack`|Show stack frames|`info stack`|
|`bt`|Backtrace call stack|`bt`|

---

### **Debugging Shared Libraries**

|Command|Description|Example|
|---|---|---|
|`info shared`|Show loaded libraries|`info shared`|
|`catch load <lib>`|Break when library loads|`catch load libc.so.6`|
|`set environment <var>=<value>`|Set environment variable|`set env PATH=/tmp`|

---

### **Debugging Threads**

|Command|Description|Example|
|---|---|---|
|`info threads`|Show running threads|`info threads`|
|`thread <num>`|Switch to thread|`thread 2`|
|`thread apply all bt`|Backtrace all threads|`thread apply all bt`|

---

### **Exploit Development & Pattern Generation**

|Command|Description|Example|
|---|---|---|
|`gef pattern create <size>`|Generate cyclic pattern|`gef pattern create 100`|
|`gef pattern offset <value>`|Find offset in pattern|`gef pattern offset 0x61616162`|
|`info frame`|Get frame info (canary, saved EIP)|`info frame`|

---

### **GDB Scripting**

|Command|Description|Example|
|---|---|---|
|`source <file>`|Load GDB script|`source script.gdb`|
|`define <cmd>`|Create a custom command|`define mycmd`|
|`document <cmd>`|Add command description|`document mycmd`|
|`shell <cmd>`|Run a shell command|`shell ls`|

---

### **GDB with Plugins (GEF, PEDA, pwndbg)**

|Command|Description|Example|
|---|---|---|
|`gef`|Load GEF plugin|`gef`|
|`peda`|Load PEDA plugin|`peda`|
|`pwndbg`|Load pwndbg plugin|`pwndbg`|

---

## **Exploit Tricks**

|Trick|Command|Example|
|---|---|---|
|**Find buffer overflow offset**|`pattern create <size>` & `pattern offset <value>`|`pattern create 200`|
|**Check for NX (No eXecute) bit**|`checksec`|`checksec ./binary`|
|**Modify return address**|`set $rip = <addr>`|`set $rip = 0x4005d4`|
|**Modify function return value**|`return <val>`|`return 0`|
|**Call a function manually**|`call <func>(<args>)`|`call system("/bin/sh")`|

---
