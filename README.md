
# Hardware Tick-to-Book: NASDAQ ITCH 5.0 Engine

![Language](https://img.shields.io/badge/Language-SystemVerilog-blue)
![Verification](https://img.shields.io/badge/Verification-cocotb%20%7C%20Python-green)
![Status](https://img.shields.io/badge/Status-Planned%20(Pre--Development)-lightgrey)

## Overview
This repository will house a cycle-accurate, hardware-accelerated Level 2 Order Book engine designed to process the NASDAQ ITCH 5.0 protocol. Bypassing traditional software network stacks, the goal of this RTL pipeline is to ingest raw PCAP network data, decode financial messages, and maintain a sorted Bid/Ask spread entirely in hardware. 

This project is structured as a 5-week development sprint to demonstrate ultra-low latency design principles, complex state management in FPGAs, and robust software-driven hardware verification.

## Project Roadmap (5-Week Sprint)
- [ ] **Week 1: Architecture & Network Ingress**
  - Define datapath and BRAM memory map.
  - Implement raw UDP/IP payload extraction and asynchronous clock domain crossing FIFOs.
- [ ] **Week 2: Protocol Decoder**
  - Build zero-stall state machines to parse ITCH 5.0 messages (Add, Execute, Cancel).
- [ ] **Week 3: Hardware Order Book**
  - Implement custom memory architecture to track outstanding orders and maintain the top-of-book (BBO).
- [ ] **Week 4: Software Reference Model**
  - Develop a software-based Python order book to process historical PCAP files for baseline comparison.
- [ ] **Week 5: Co-Simulation & SVA Integration**
  - Integrate `cocotb` to drive PCAP data directly into RTL. 
  - Embed SystemVerilog Assertions (SVA) and verify zero data loss.

## Planned Architecture 
The datapath will be fully pipelined and segmented into three primary modules:
*   **Network Ingress & Framing:** Extracts raw ITCH payloads, managing clock crossings via custom Gray-code FIFOs.
*   **Protocol Decoder:** Parses ITCH 5.0 messages and extracts required fields (Stock Locate, Reference Number, Price, Shares).
*   **Hardware Order Book:** A custom BRAM-based memory architecture to track orders and handle modifications instantly.

## Planned Verification Methodology
Physical deployment will be simulated using a rigorous, data-driven testbench environment utilizing Python, `cocotb`, and real-world NASDAQ PCAP files for cycle-by-cycle comparisons against a Python reference model.
*   `docs/`: Timing diagrams and memory map architecture notes.
