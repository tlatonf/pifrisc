# SS2: TOOLS AND ENVIRONMENTS

*Latest update: 2024-10-28.*

## 1. Linux & Git

- In this section, you will have to research how to use them yourself. You can refer to the following documents:
  - [Các lệnh cơ bản trong Linux - 35 Linux Commands cần biết](https://www.hostinger.vn/huong-dan/cac-lenh-co-ban-trong-linux)
  - [Introduction to Git](https://videotutorials.notion.site/Introduction-to-Git-ac396a0697704709a12b6a0e545db049)
  - [Từ gà tới pro Git và Github trong 20 phút - Tự học Git siêu tốc](https://www.youtube.com/watch?v=1JuYQgpbrW0)

## 2. Guide to Setting Up a Virtual Machine

- Download and install [Vmware Workstation Pro 17.5.2](https://softwareupdate.Vmware.com/cds/vmw-desktop/ws/17.5.2/23775571/windows/core/). You can find an activation key [here](https://github.com/hegdepavankumar/Vmware-Workstation-Pro-17-Licence-Keys). *Skip if you have installed it previously.*

- Download and extract the virtual machine [Durian]() containing Cadence Xcelium 20.09 *(it has a size of about 25GB)*. You should refer to the guide before extracting: [How to Extract Multi-Part Archive Files](https://www.toolfarm.com/knowledge-base/licensing/how-to-extract-multi-part-archive-files/).

## 3. Guide to Mounting a Shared Folder from Windows to the Virtual Machine *(skip if you don't need to exchange files between them)*

- Open Vmware -> Access `Settings` in the `VM section` on the Menu bar -> Select `Shared Folders Setting` in the `Option tab` -> Click to select `Always enabled` and add a Shared Folder.

  ![1](./img/1.png)

- Choose the folder in Windows that you want to mount with the virtual machine. The default name of the interface is `Mount`. If you want to change it to a different name, you need to edit the `.bashrc` file located at `~/.bashrc`.

- To proceed with mounting, you just need to execute the command below in the terminal of the virtual machine.

  ```bash
  $ vmhgfs-fuse -o auto_unmount .host:/Mount ~/Mount
  ```

  Alternatively, you can run the aliased command below.

  ```bash
  $ mount
  ```

## 4. Connect via SSH to the Virtual Machine *(skip if you don't need to use an external editor)*

- Find the IP address of the virtual machine, you can do this by executing the command:

  ```bash
  $ ip -4 addr show ens33 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
  ```

  ![2](./img/2.png)

  You may also follow the instructions in the image below:

  ![5](./img/5.png)

- You can use the `Windows Terminal` or `VSCode` to connect via SSH to the virtual machine using the syntax:

  ```bash
  $ ssh <username>@<ip-address>
  ```

  Example:

  ```bash
  $ ssh pifer@192.168.127.100
  ```

- If it displays like below, it means you have successfully connected. Now you can `Run Vmware in the background`.

  ![3](./img/3.png)

- Note: On each start of Vmware, the `ip-address` may change. You can set a static IP address for convenience in connecting.

## 5. Run the Sample Project

### 5.0. Design Flow

> *(Excerpt from Lab 0 - SystemVerilog, Computer Architecture Courses)*
>
> ![4](./img/4.png)
>
> Figure 1 shows the basic design flow of design a digital logic block. In this diagram, designers have to follow four steps:
>
> 1. **RTL Coding** is consisted of designing algorithms, FSMs, etc. to handle the requirements of the problem or expected designs. In this document, you will use SystemVerilog HDL, a versatile HDL for both design and verification.
> 2. **Lint Check** is a process of static code analysis to check the quality of the code. Lint Check will check your code with a list of rules, to find any violations syntax errors or potential code lines or blocks that may cause errors or bugs when running. This step is needed to perform right after you finish RTL Coding. If there are any flags or errors, you need to read them carefully to know exactly the rules you violated to fix your code.
> 3. **Verification** is a process of running your code to check correctness your design. Based on the requirements, each input will have only one expected output, so you have to interpret the log or the waveform generated from this step to fix your design. After fixing your design, don't forget linting again.
> 4. **Implementation** is to implement the design into real hardware. Your simulation and the reality are sometimes not the same.

### 5.1. Execute cloning of the `sample_project`:

```bash
$ cp -r /vault/sample_project/ ~/
```

### 5.2. Run lint-check:

```bash
$ cd ~/sample_project/20_sim/
$ ./linting.sh
```

* There will be a small bug when running `./linting.sh`, please find a way to fix it!

  ```bash
  $ pifer@pifclub:20_sim$ cd ~/sample_project/20_sim/
  $ pifer@pifclub:20_sim$ ./linting.sh
  TOOL:   xrun    20.09-s001: Started on Oct 28, 2024 at 09:12:34 PDT
  TOOL:   xrun(64)        20.09-s001: Started on Oct 28, 2024 at 09:12:34 PDT
  xrun(64): 20.09-s001: (c) Copyright 1995-2020 Cadence Design Systems, Inc.
  file: ../00_src/ic74138.sv
          module worklib.ic74138:sv
                  errors: 0, warnings: 0
                  Caching library 'worklib' ....... Done
          Elaborating the design hierarchy:
          Top level design units:
                  ic74138
  xmelab: *W,DSEMEL: This SystemVerilog design will be simulated as per IEEE 1800-2009 SystemVerilog simulation semantics. Use -disable_sem2009 option for turning off SV 2009 simulation semantics.
          Building instance overlay tables: .................... Done
          Generating native compiled code:
                  worklib.ic74138:sv <0x45550e4d>
                          streams:   1, words:   536
          Building instance specific data structures.
          Loading native compiled code:     .................... Done
          Design hierarchy summary:
                           Instances  Unique
                  Modules:         1       1
                  Registers:       1       1
                  Scalar wires:    3       -
                  Vectored wires:  1       -
                  Always blocks:   1       1
          Writing initial simulation snapshot: worklib.ic74138:sv
  hal(64): 20.09-s001: (c) Copyright 1995-2020 Cadence Design Systems, Inc.
  hal: Options:   -cdslib ./xcelium.d/run.lnx8664.20.09.d/cds.lib -logfile xrun.log -f /home/pifer/sample_project/20_sim/xcelium.d/run.lnx8664.20.09.d/hal.args .
  hal: Snapshot:  worklib.ic74138:sv.
  hal: Workspace: /home/pifer/sample_project/20_sim.
  hal: Date: Mon Oct 28 09:13:07 PDT 2024.
  
  Performing lint checks
  .
  Performing synthesizability checks
  .
  Performing structural checks
  .
  
  Analysis summary :
  
   Warnings : (6)
    CDEFCV (1)      DSEMEL (1)      NOBLKN (1)      STYVAL (2)
    TPOUNR (1)
  
   Notes    : (2)
    NUMDFF (1)      PRTCNT (1)
  
  Analysis complete.
  
  Complete HAL log in : xrun.log
  To analyze results, run following command :
      xmbrowse -64bit -cdslib ./xcelium.d/run.lnx8664.20.09.d/cds.lib -hdlvar ./xcelium.d/run.lnx8664.20.09.d/hdl.var -sortby severity -sortby category -sortby tag xrun.log
  
  TOOL:   xrun(64)        20.09-s001: Exiting on Oct 28, 2024 at 09:15:16 PDT  (total: 00:02:42)
  ```

* According to the results above, the RTL code has **6 warnings** and **2 notes**; the detailed report is saved in the file `xrun.log`:

  ```bash
  $ cat ~/sample_project/20_sim/xrun.log

### 5.3. Run testbench:

```bash
$ cd ~/sample_project/20_sim/
$ ./testbench.sh
```

Result:

```bash
pifer@pifclub:20_sim$ ./testbench.sh
TOOL:   xrun    20.09-s001: Started on Oct 28, 2024 at 09:27:13 PDT
TOOL:   xrun(64)        20.09-s001: Started on Oct 28, 2024 at 09:27:13 PDT
xrun(64): 20.09-s001: (c) Copyright 1995-2020 Cadence Design Systems, Inc.
file: ../00_src/ic74138.sv
        module worklib.ic74138:sv
                errors: 0, warnings: 0
file: ../10_tb/ic74138_tb.sv
        module worklib.ic74138_tb:sv
                errors: 0, warnings: 0
                Caching library 'worklib' ....... Done
        Elaborating the design hierarchy:
        Top level design units:
                ic74138_tb
xmelab: *W,DSEMEL: This SystemVerilog design will be simulated as per IEEE 1800-2009 SystemVerilog simulation semantics. Use -disable_sem2009 option for turning off SV 2009 simulation semantics.
        Building instance overlay tables: .................... Done
        Generating native compiled code:
                worklib.ic74138:sv <0x0b9d4e16>
                        streams:   1, words:   613
                worklib.ic74138_tb:sv <0x153068f8>
                        streams:   5, words:  7239
        Building instance specific data structures.
        Loading native compiled code:     .................... Done
        Design hierarchy summary:
                              Instances  Unique
                Modules:              2       2
                Registers:           10      10
                Scalar wires:         3       -
                Vectored wires:       3       -
                Always blocks:        1       1
                Initial blocks:       1       1
                Pseudo assignments:   4       4
        Writing initial simulation snapshot: worklib.ic74138_tb:sv
Loading snapshot worklib.ic74138_tb:sv .................... Done
xmsim: *W,DSEM2009: This SystemVerilog design is simulated as per IEEE 1800-2009 SystemVerilog simulation semantics. Use -disable_sem2009 option for turning off SV 2009 simulation semantics.
xcelium> source /opt/cadence/installs/XCELIUM2009/tools/xcelium/files/xmsimrc
xcelium> run
Testcase # 1  | g1 = x, g2a = 1, g2b = x | decoder = 11111111, decoder_tc = 11111111 | PASSED
Testcase # 2  | g1 = x, g2a = x, g2b = 1 | decoder = 11111111, decoder_tc = 11111111 | PASSED
Testcase # 3  | g1 = 0, g2a = x, g2b = x | decoder = 11111111, decoder_tc = 11111111 | PASSED
Testcase # 4  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11111110, decoder_tc = 11111110 | PASSED
Testcase # 5  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11111101, decoder_tc = 11111101 | PASSED
Testcase # 6  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11111011, decoder_tc = 11111011 | PASSED
Testcase # 7  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11110111, decoder_tc = 11110111 | PASSED
Testcase # 8  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11101111, decoder_tc = 11101111 | PASSED
Testcase # 9  | g1 = 1, g2a = 0, g2b = 0 | decoder = 11011111, decoder_tc = 11011111 | PASSED
Testcase #10  | g1 = 1, g2a = 0, g2b = 0 | decoder = 10111111, decoder_tc = 10111111 | PASSED
Testcase #11  | g1 = 1, g2a = 0, g2b = 0 | decoder = 01111111, decoder_tc = 01111111 | PASSED
Simulation complete via $finish(1) at time 110 NS + 0
../10_tb/ic74138_tb.sv:57     $finish;
xcelium> exit
TOOL:   xrun(64)        20.09-s001: Exiting on Oct 28, 2024 at 09:27:35 PDT  (total: 00:00:22)
```