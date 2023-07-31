# riscv_ctb_challenges
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/7c9dab74-95db-40dc-a5f7-83adbe73dc15)


This repository is a complete documentation and a summary of the work performed by Archita Malgaonkar during the [RISC-V Capture The Bug Hackathon]


This workshop by Vyoma Systems was conducted to identify the bugs, report them and solve them and generate a bug-free instruction set architecture of RISC-V. The workshop aims more at the verification factor of RISC-V processor.


# Table of Contents
  * [Level-1](#Level-1)
  * [Level-2](#Level-2)
  * [Refrences](#Refrences)
  
# Level-1
## Challenge-1 logical

- Task was to identify the bug , reprogram and generate a spike file.
- For running the command we make the use of 'make' command.

### The bugs reported
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/9cd81136-4043-41a2-8aa0-29496beb77ba)


- The bug here identified was `and` instruction requires both its operators to be registers.
- z4 is not a register as defined in the architecture of RISC-V.
- To correct the bug, `and` is an R-Format ISA, so we replaced z4 with any defined registers in RV32I, like t0. So final instruction of line 15855 in `test.S` file in `and s7,ra,t0`.
- The next bug reported was for `addi`. the `i` in the add instruction specifies that one operand should be an immediate value.
- s0 is not immediate data, so we replace s0 with any immediate data like 2. So final instruction of line no 25584 in `test.S` file in `addi s5,t1,2`.
- 
  
#### Defined Registers in RV32I


#### add instruction
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/f8c033b6-7ada-4743-98aa-047ca46b298a)


#### addi instruction

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/5eca11b1-eb83-4d49-a85c-f822ef52cb99)


- Then we run the make command, which generates `test.disass`,`test.elf` and `test_spike.dump` files.
  
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/7d2d4766-2bbb-466a-9522-a8e6b9f38d9c)


## Challenge-2 logical

- To find the bug we ran `make` command and found the loop was running infinite times, so we came out of the loop using `Ctrl+c` and `q` and tried to find the bug.
  

- Task was to identify the bug , reprogram and generate a spike file.
- For running the command we make the use of 'make' command.

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/24d5aa54-41a0-43c5-9014-059c2a86a07e)



### The bugs reported
- The program runs in an infinite loop. The program reported was the loop was not getting decremented.
- Adding some commands to the program to decrement the loop .
- Finally, the required files were generated after running' make'.
- 
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/a0dc242f-f883-4487-997a-899b9d78e3e1)



## Challenge-3 illegal

- To find the bug we ran `make` command and found the loop was running infinite times, so we came out of the loop using `Ctrl+c` and `q` and tried to find the bug.
  


### The bugs reported
- There was a handler code and an interrupt code.
- The bug reported was the CSR was not getting incremented


- Finally, the required files were generated after running' make'.
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/a11380fd-bfec-444a-a2b0-043b6400b99c)

## Level-1 Refrences 
- [RISC-V Tests]([https://www.youtube.com/watch?v=mbyb7BgYyXg)](https://youtu.be/mbyb7BgYyXg)
- [rircv-test GitHub]([https://github.com/riscv-software-src/riscv-tests](https://www.google.com/url?q=https://github.com/riscv-software-src/riscv-tests&sa=D&source=apps-viewer-frontend&ust=1690897725906011&usg=AOvVaw137g2g_y4HBnjO4WgFlOkB&hl=en))
- [RISC-V Instructions](https://youtu.be/bp-Y7nSJa8o)

# Level-2 Instructions AAPG Random Tests
## Challenge-1 

- Some illegal commands were generated.
- `make` command exposes the problem.

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/9cefe160-78cf-4d54-8e40-75586ce4e492)


###  Bugs reported
- To find the bug, we went through the `rv32i.yaml` file and found an ISA-instruction distribution of 64 bits, initialized to 10 but working in rv32i, so we changed it to 0.
- ctrl instructions were set to 0.
  
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/2942cd68-83de-41ea-b4f4-32ebfcbfefa4)

- We changed `rel_rv64m: 10` to `rel_rv64m: 0` to correct the bug.
- Finally, after running `make` the required files were generated.

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/0f2748f7-6b23-43ef-92e2-65fa98c993cd)


## Challenge-2 exceptions

- To find the bug, we ran the `make` command and found it generated only one illegal exception.
- The task here is to generate 10 illegal instructions


![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/a0617d2a-d7d6-49e4-8b10-7895b5cb9ec5)

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/e570eb9c-adc0-4a4b-a574-1bd78d0ad51e)


### Bugs reported
- Here, we need to generate 10 illegal exceptions, so we made some changes in the `rv32i.yaml` file.
- Changed `total_instructions: 1000` reduced it to `total_instructions: 200`, `rel_rv32i.data: 10` to `rel_rv32i.data: 0` ,  `rel_rv32m: 0` to `rel_rv32m: 1` and `ecause00: 0` to `ecause00: 1`.


- Finally, after running the `make` command to generate all illegal exceptions, which are saved in generated `exception.log` file.
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/7bfd8820-6d40-4bbe-95d4-1828dcfc194c)

#### Generated illegal exception.
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-Archita0102/assets/66164675/275c042e-0822-4b76-bd67-dbcb39ac3353)




## Level-2 Refrences 
- [Automated Assembly Program Generator]([https://gitlab.com/shaktiproject/tools/aapg](https://gitlab.com/shaktiproject/tools/aapg))
- [Wiki AAPG]([https://gitlab.com/shaktiproject/tools/aapg/-/wikis/Wiki-AAPG-%5B2.2.2%5D](https://gitlab.com/shaktiproject/tools/aapg/-/wikis/Wiki-AAPG-%5B2.2.2%5D)https://gitlab.com/shaktiproject/tools/aapg/-/wikis/Wiki-AAPG-%5B2.2.2%5D)


## Acknowledgement

- I would like to express by gratitude to Vyoma Systems, Lavanya J for guiding throughout the hackathon.
- (https://vyomasystems.com/)

