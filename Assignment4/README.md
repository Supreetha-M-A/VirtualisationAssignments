# CMPE283 : Virtualization Technologies

# Assignment 4

Pre-requistes:
Requires a working correctly assignment3 configuration

### Q1  For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched

1. Work done by Satish Kathiriya:  
  • Executed assignment 3 code and output taken for Nested paging (ept = 1).
 
2. Work done by Supreetha M A:

  • Executed assignment 3 code and output taken for Shadow Paging (ept = 0).
 
 Together we analyzed the output and answered the questions 

### Q2 Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.

Verified: Assignment 3 code is functional.

#### Step 1: 
Open virt-manager and start virtual machine. Run case 3 from previous assignment (To print all exit type wise counts). 

#### Step 2: 
Try dmesg (for ept i.e nested paging)

#### Step 3:
execute below commands to switch from nested paging to shadow paging:  

```
sudo rmmod kvm_intel && sudo rmmod kvm && sudo modprobe kvm && sudo modprobe kvm_intel ept=0

Reboot
```

### Step 4:
Try dmesg (without ept i.e Shadow paging)

### Q3 What did you learn from the count of exits? Was the count what you expected? If not, why not?

-	In the case of shadow paging, we observe that, maximum exit occurred of type “CR_ACCESS ".
-	Also, INVLPG exit is present in case of shadow paging. (INVLPG exit is used by hypervisor to invalidate translation in the TLB).

### Q4 What changed between the two runs (ept vs no-ept)?

Nested Paging (ept=1)				
1. The VM exits for “EPT_VIOLATION”	
2. The VM exits for “EPT_MISCONFIG”	
									
Shadow Paging (ept=0)
1. The VM exits for “INVALPG”
2. Count of exits for reason “CR_ACCESS” increased significantly
3. Exit count seen for “XSETBV”

-	In case of shadow paging the count of exits for reason “CR_ACCESS” increased significantly as hypervisor takes exits on access of CR register
