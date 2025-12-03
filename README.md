# AHB Protocol Verification – SystemVerilog OOP Testbench  
[![SV](https://img.shields.io/badge/SystemVerilog-OOP-blue)]() 
[![AHB](https://img.shields.io/badge/AMBA-AHB-green)]()
[![Vivado](https://img.shields.io/badge/Simulator-Vivado%20XSIM-orange)]()
[![Status](https://img.shields.io/badge/Project-Passed-brightgreen)]()
[![License](https://img.shields.io/badge/Code-Open--Source-lightgrey)]()

This repository contains a **SystemVerilog OOP-based verification environment** for an **AMBA AHB Slave**.  
It demonstrates constrained-random stimulus generation, functional checking, mailbox communication, and layered testbench architecture (similar to UVM but using pure SV).

---

## 🚀 Features
- Supports **Single**, **INCR4/8/16**, **WRAP4/8/16**, and **Unspecified Length** burst transfers  
- Full AHB pipelined protocol: `HTRANS`, `HWRITE`, `HSIZE`, `HBURST`, `HREADY`, `HRESP`  
- Self-checking testbench with Scoreboard  
- Layered OOP architecture:
  - **Interface**
  - **Transaction**
  - **Generator**
  - **Driver**
  - **Monitor**
  - **Agent**
  - **Environment**
  - **Scoreboard**

---

## 📂 Project Structure

