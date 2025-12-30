---
layout: default
title: Labs & Exercises
nav_order: 5
permalink: /docs/labs/
has_children: true
---

# Laboratory Exercises

Hands-on lab exercises to reinforce course concepts and develop practical FPGA design skills.

---

## Lab Structure

Each lab includes:
- **Objective**: What you'll accomplish
- **Pre-lab**: Preparation and reading
- **Procedure**: Step-by-step instructions
- **Deliverables**: What to submit
- **Grading Rubric**: How you'll be evaluated

---

## Combinational Logic Labs

### [Lab 1: Introduction to Verilog HDL](labs/combinational/lab1)
**Week 1-2** | Learn Verilog basics and FPGA design flow
- SystemVerilog vs Verilog
- Design flow and simulation
- FPGA synthesis and programming
- LED control circuits

### [Lab 2: Logic Gates and Truth Tables](labs/combinational/lab2)
**Week 2-3** | Implement basic logic gates
- AND, OR, NOT, NAND, NOR, XOR gates
- Truth table verification
- Multi-level logic circuits
- Testbench development

### [Lab 2a: Seven-Segment Display](labs/combinational/lab2a)
**Week 3** | Build 7-segment display decoder
- BCD to 7-segment decoder
- Hexadecimal display
- Display multiplexing

### [Lab 3: Multiplexers and Decoders](labs/combinational/lab3)
**Week 3-4** | Design combinational building blocks
- 4:1 and 8:1 multiplexers
- 2:4 and 3:8 decoders
- Priority encoders

### [Lab 3a: Adders and Arithmetic](labs/combinational/lab3a)
**Week 4-5** | Implement arithmetic circuits
- Half-adder and full-adder
- 4-bit ripple-carry adder
- Carry lookahead logic
- ALU design

### [Lab 4: K-Map Minimization and Optimization](labs/combinational/lab4)
**Week 5** | Practice logic minimization
- 3-variable and 4-variable K-maps
- Don't care conditions
- Logic optimization techniques

---

## Sequential Logic Labs

### [Lab 5: Flip-Flops and Registers](labs/sequential/lab5)
**Week 6-7** | Study sequential storage elements
- D, JK, T flip-flops
- Edge-triggered behavior
- Register design
- Setup and hold time analysis

### [Lab 5a: Introduction to FSMs](labs/sequential/lab5a)
**Week 7** | Introduction to state machines
- FSM concepts (Moore vs Mealy)
- Simple sequence detector
- State diagram design

### [Lab 6: Counters and Timers](labs/sequential/lab6)
**Week 7-8** | Design and implement counters
- Binary up/down counter
- Modulo-N counter
- BCD counter
- Digital clock design

### [Lab 7: Finite State Machines](labs/sequential/lab7)
**Week 8-9** | Build complex state machines
- Traffic light controller
- Vending machine FSM
- Sequence detectors
- Protocol controllers

### [Lab 8: Memory and Advanced Topics](labs/sequential/lab8)
**Week 10-11** | Work with memory and advanced concepts
- ROM and RAM design
- FIFO buffer implementation
- Memory interfacing
- Clock domain crossing

---

## Advanced Labs

### [Lab 9: Memory Systems](advanced/lab09/)
**Module 10** | Work with memory structures
- RAM implementation
- FIFO buffer design
- ROM-based lookup table

### [Lab 10: Clock Domain Crossing](advanced/lab10/)
**Module 11** | Handle multiple clock domains
- Synchronizer design
- Asynchronous FIFO
- Handshake protocols

### [Lab 11: Pipelined Design](advanced/lab11/)
**Module 11** | Optimize for performance
- Pipelined multiplier
- Throughput vs latency analysis
- Timing closure

---

## Lab Policies

### Equipment
- FPGA boards available for checkout
- Lab computers with Quartus installed
- Remote access available for simulation

### Lab Hours
- **When**: [Days/Times]
- **Where**: [Lab Location]
- **TAs**: Available for assistance

### Submission
- Due dates: See course schedule
- Submit via Canvas
- Include: Code, screenshots, report

### Grading
- **Pre-lab**: 10%
- **Implementation**: 50%
- **Testing/Demo**: 25%
- **Report**: 15%

---

## Lab Resources

### Equipment Guides
- [DE10-Lite Quick Reference](../resources/DE10-Lite_quickref.pdf)
- [Oscilloscope Tutorial](../resources/scope_tutorial.pdf)
- [Logic Analyzer Guide](../resources/logic_analyzer.pdf)

### Software
- [Quartus Workflows](../resources/quartus_workflows.pdf)
- [ModelSim Commands](../resources/modelsim_ref.pdf)
- [Debugging Techniques](../resources/debugging.pdf)

### Templates
- [Lab Report Template](../resources/lab_report_template.docx)
- [Verilog Module Template](../resources/verilog_template.v)
- [Testbench Template](../resources/testbench_template.v)

---

## Safety & Best Practices

### Lab Safety
- No food or drink near equipment
- Handle boards by edges
- Report damaged equipment immediately
- Keep workspace organized

### Design Best Practices
- Always save your work frequently
- Use version control (Git)
- Comment your code
- Test incrementally
- Back up to cloud storage

### Debugging Tips
1. Start with simulation before hardware
2. Use SignalTap for on-chip debugging
3. Check pin assignments carefully
4. Verify timing constraints
5. Read error messages completely

---

## Getting Help

### During Lab Hours
- Ask TA for assistance
- Work with lab partners
- Use available documentation

### Outside Lab
- Post on discussion board
- Attend office hours
- Email instructor with specific questions

---

**Ready to start? Check the [schedule](../syllabus/) for your first lab!**
