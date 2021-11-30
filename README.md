# CMPE283 : Virtualization Technologies

# Assignment 3

Pre-requistes:
Requires a working correctly assignment2 configuration

### Q1

1. Work done by Supreetha M A:  
  • Created leaf node %eax= 0x4FFFFFFE for case 2
  • Made required changes in cpuid.c and vmx.c
  •	Installed cpuid Pakage on inner VM
  •	Tested and Verified results
  •	Documented the steps and results.
 
2. Work done by Satish Kathiriya:  
  •	Created leaf node %eax= 0x4FFFFFFC for case 4
  •	Made required changes in cpuid.c and vmx.c
  •	Tested and Verified results
  •	Documented the steps and results.


### Q2
Steps to run the assignment:

### Step 1: Add code to KVM at file /linux/arch/x86/kvm/vmx/vmx.c and /linux/arch/x86/kvm/cpuid.c

1. For CPUID leaf node %eax= 0x4FFFFFFE: 
Return the total time spent processing all exits %ebx and %ecx.
2. For CPUID leaf node %eax= 0x4FFFFFFC:
Return the total time spent for that exit for that exit number in %ebx and %ecx.

### Step 2: Build the updated code:  
```
make modules
make modules_install
make install
Reboot
```	

### Step 3: Open virt-manager and start virtual machine. Install CPUID package inside the inner vm. 
```sudo apt-get install cpuid```
 
### Step 4: Test the code using below commands for case 1:
1. run	```cpuid -l 0x4FFFFFFE```
2. Try dmesg command in the host system’s terminal
Total exits taken for VM reboot:  510,143

### Step 5: Test the code using below commands for case 2:

1. run ```cpuid -l 0x4FFFFFFC s -32``` , and ```dmesg``` command in the host system’s terminal to view count of all available exits.
2. can run ```cpuid -l 0x4FFFFFFC s -444``` to test output for invalid exit code.
3. Also can run ```cpuid -l 0x4FFFFFFC s -3``` to test the output for valid exit but not implemented by KVM.

### Q3

Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there
more exits performed during certain VM operations? Approximately how many exits does a full VM
boot entail?

The frequency of the time spent on exit mainly depends on the type of exit. Exits do not increase at a stable rate. When system performs more previleged operations then number of exits increases.

### Q4

Of the exit types defined in the SDM, which are the most frequent? Least?

In our case CPUID (10) - [137,689], and  I/O instruction (30) -- [214,784] were more frequent. MOV DR (29) - 2, instruction was least frequent.
