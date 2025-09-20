# Tool Installation Guide

This guide shows how to install and verify the essential tools needed for RISC-V SoC tapeout work. For each tool, use the provided installation command and check the included screenshot to verify proper installation.

---

## 1. Yosys (Open SYnthesis Suite)

**Install Command:**
```bash
sudo apt update
sudo apt install yosys -y
```

After installing, run:
```bash
yosys
```
You should see output as below:

![Yosys verification](week_0/image1.png)

---

## 2. Icarus Verilog (iverilog)

**Install Command:**
```bash
sudo apt install iverilog -y
```

After installing, run:
```bash
iverilog
```
You should see output as below:

![Icarus Verilog verification](images/image2.png)

---

## 3. GTKWave

**Install Command:**
```bash
sudo apt install gtkwave -y
```

After installing, run:
```bash
gtkwave
```
You should see the GTKWave GUI as below:

![GTKWave verification](images/image3.png)

---

## 4. Ngspice

**Install Command:**
```bash
sudo apt install ngspice -y
```

After installing, run:
```bash
ngspice
```
You should see output as below:

![Ngspice verification](images/image4.png)

---

## 5. Magic VLSI

**Install Command:**
```bash
sudo apt install magic -y
```

After installing, run:
```bash
magic
```
You should see the Magic VLSI GUI as shown below:

![Magic VLSI verification](images/image5.png)

---

## Summary

Make sure each tool launches and displays output similar to the screenshots. These open-source tools are essential for digital and analog design, simulation, synthesis, and layout in your RISC-V SoC projects.
