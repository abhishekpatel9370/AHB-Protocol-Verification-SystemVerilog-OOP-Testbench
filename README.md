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

AHB-PROTOCOL-VERIFICATION/
│
├── rtl/
│   └── ahb_slave.sv
│
├── tb/
│   ├── ahb_if.sv
│   ├── transaction.sv
│   ├── generator.sv
│   ├── driver.sv
│   ├── monitor.sv
│   ├── scoreboard.sv
│   ├── agent.sv
│   ├── environment.sv
│   └── tb.sv
│
└── waves/
    └── waveform.png




---

## 🧪 Verification Architecture

### 🔹 **Transaction**
Encapsulates:
- Address  
- Data  
- Size  
- Burst type  
- Write/Read  
- Unspecified-length count  

Includes `copy()` for mailbox transfer.

---

### 🔹 **Generator**
- Randomizes transactions  
- Sends them to driver through `mailbox #(transaction)`  
- Uses handshake events:
  - `drvnext` – driver completed  
  - `sconext` – scoreboard completed  
- `count` decides how many transactions to run

---

### 🔹 **Driver**
Implements AHB protocol:
- Drives all AHB signals  
- Handles:
  - SINGLE  
  - INCR 4/8/16  
  - WRAP 4/8/16  
  - UNSPECIFIED LENGTH  
- Waits for handshake using `@(posedge hready)`  
- Generates reset sequence

---

### 🔹 **Monitor**
Passive checker that samples interface:
- Captures address + data  
- Sends to scoreboard  
- Extracts `next_addr` from slave for wrap/incr validation

---

### 🔹 **Scoreboard**
Implements a reference memory model:
- For write: updates model  
- For read: compares expected data with DUT output  
- Reports:
  -  DATA MATCHED  
  -  DATA MISMATCHED  
  -  EMPTY LOCATION READ  

---

### 🔹 **Agent**
Combines:
- Generator  
- Driver  
- Monitor  
Connects:
- Mailboxes  
- Virtual interface  
- Synchronization events  

---

### 🔹 **Environment**
Top-level verification block.  
Instantiates:
- Agent  
- Scoreboard  

Runs both in parallel with:
```systemverilog
env.run();

Testbench (tb.sv)

Creates interface & DUT

Creates environment

Drives clock

Runs verification automatically

Stops when generator finishes

▶ Sample Output Log
[DRV] : WRAP8 TRANSFER ADDR : 12 DATA : 5
[MON] : addr : 5 data : 12
[SCO] : DATA WRITE

[DRV] : SINGLE READ TRANSFER ADDR : 5
[MON] : SINGLE TRANSFER READ addr : 5 data : 12
[SCO] : DATA MATCHED

🛠 Tools Used

SystemVerilog

Vivado XSIM (2023/2024/2025 versions compatible)

Object-Oriented Testbench Architecture

📌 Future Improvements

Functional coverage

Error response (SPLIT, RETRY, ERROR) verification

Random back-pressure (HREADY low cycles)

Full UVM migration

👤 Author

Abhishek Patel
VLSI | RTL | Verification
LinkedIn Profile:https://www.linkedin.com/in/abhishek-patel-6b5428266/
