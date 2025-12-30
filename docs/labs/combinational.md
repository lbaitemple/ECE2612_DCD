---
layout: default
title: Combinational Logic Labs
parent: Labs & Exercises
nav_order: 1
has_children: true
permalink: /docs/labs/combinational/
---

# Combinational Logic Labs

Hands-on laboratory exercises focusing on combinational circuit design, Verilog HDL programming, and FPGA implementation.

---

## Lab Overview

These labs cover fundamental concepts in combinational logic design:
- Verilog/SystemVerilog programming
- Logic gate implementation
- Testbench development
- Seven-segment display interfacing
- Encoders and decoders
- Error correction codes
- FPGA synthesis and testing

---

## Lab Sequence

| Lab | Title | Week | Topics |
|-----|-------|------|--------|
| [Lab 1](lab1) | Introduction to Verilog HDL | 1-2 | Gate primitives, design flow, simulation |
| [Lab 2a](lab2a) | Introduction to Testbenches | 3 | Self-checking testbenches, verification |
| [Lab 2](lab2) | Encoder Design (ECC) | 4 | Hamming(7,4) encoder, XOR parity |
| [Lab 3a](lab3a) | Connecting to DE10-Lite | 5 | QSF files, pin assignments, I/O mapping |
| [Lab 3](lab3) | Seven-Segment Display | 6 | BCD decoder, hex display, case statements |
| [Lab 4](lab4) | Hamming(7,4) Decoder | 7 | Error correction, syndrome detection |

---

## Learning Path

```
Lab 1: Verilog Basics & Gates
    ↓
Lab 2a: Testbench Development
    ↓
Lab 2: Hamming Encoder (Apply XOR, combinational design)
    ↓
Lab 3a: Hardware Connections (Learn pin assignments)
    ↓
Lab 3: Seven-Segment Display (Case statements, hardware I/O)
    ↓
Lab 4: Hamming Decoder (Complete ECC system)
    ↓
→ Sequential Logic Labs
```

---

## Lab Format

Each lab includes:
- **Learning Objectives**: What you'll master
- **Prerequisites**: Required knowledge
- **Procedure**: Step-by-step instructions
- **Deliverables**: What to submit
- **Checkoff Requirements**: In-person demonstration
- **Grading Rubric**: Assessment criteria

---

## Required Equipment

- **FPGA Board**: Terasic DE10-Lite (Intel MAX 10 FPGA)
- **Software**: Intel Quartus Prime Lite Edition 23.1std
- **Simulator**: ModelSim-Intel Starter Edition (included with Quartus)
- **Computer**: Windows, macOS, or Linux

---

## Submission Guidelines

All labs require:
1. **Source Code**: Verilog (.sv) files, testbenches, constraints
2. **Documentation**: Lab report (PDF) with screenshots
3. **Demonstration**: In-person checkoff with TA/instructor
4. **Video**: Optional demonstration video for remote students

---

## Tips for Success

- **Start early**: Labs build on each other
- **Test incrementally**: Don't write all code then compile
- **Use simulation first**: Verify logic before FPGA programming
- **Read error messages**: Quartus provides helpful diagnostic information
- **Ask questions**: Use office hours and discussion forums
- **Document as you go**: Take screenshots during the process

---

## Resources

- [Verilog Quick Reference](../../resources/)
- [AWS Cloud Setup](../../preparation/aws-setup/)
- [DE10-Lite Pin Assignments](../../resources/lab-resources/)

---

**Ready to start? Begin with [Lab 1: Introduction to Verilog HDL](lab1)**
