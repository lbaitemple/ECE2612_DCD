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

## Lab Categories

### [Combinational Logic Labs](combinational/)
**Labs 1-4** | Weeks 1-7

Fundamental digital design concepts including:
- Verilog HDL introduction and design flow
- Testbench development and verification
- Seven-segment display interfacing
- Error correction codes (Hamming)

| Lab | Title | Week |
|-----|-------|------|
| [Lab 1](combinational/lab1) | Introduction to Verilog HDL | 1-2 |
| [Lab 2a](combinational/lab2a) | Introduction to Testbenches | 3 |
| [Lab 2](combinational/lab2) | Encoder Design (ECC) | 4 |
| [Lab 3a](combinational/lab3a) | Connecting to DE10-Lite | 5 |
| [Lab 3](combinational/lab3) | Seven-Segment Display | 6 |
| [Lab 4](combinational/lab4) | Hamming(7,4) Decoder | 7 |

---

### [Sequential Logic Labs](sequential/)
**Labs 5-8** | Weeks 8-13

Advanced sequential circuit design including:
- Flip-flops, latches, and registers
- Shifters and barrel shifters
- Display multiplexing with counters
- Finite state machines for real devices
- Memory systems and register files

| Lab | Title | Week |
|-----|-------|------|
| [Lab 5a](sequential/lab5a) | Latches and Flip-flops | 8 |
| [Lab 5](sequential/lab5) | Shift Logic | 9 |
| [Lab 6](sequential/lab6) | Multiple Digit Display | 10 |
| [Lab 7](sequential/lab7) | Rotary Encoder | 11-12 |
| [Lab 8](sequential/lab8) | Memory Systems | 13 |

---

## Learning Progression

```
┌─────────────────────────────────────────────────────────────┐
│  COMBINATIONAL LOGIC LABS (Weeks 1-7)                       │
├─────────────────────────────────────────────────────────────┤
│  Lab 1 → Lab 2a → Lab 2 → Lab 3a → Lab 3 → Lab 4           │
│  Verilog  Testbench  ECC    Pins   7-Seg   Decoder         │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  SEQUENTIAL LOGIC LABS (Weeks 8-13)                         │
├─────────────────────────────────────────────────────────────┤
│  Lab 5a → Lab 5 → Lab 6 → Lab 7 → Lab 8                    │
│  Flip-flop Shift  Display  FSM    Memory                   │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  FINAL PROJECT (Week 14)                                    │
└─────────────────────────────────────────────────────────────┘
```

---

## Lab Policies

### Equipment
- FPGA boards available for checkout
- Lab computers with Quartus installed
- Remote access available for simulation

### Lab Hours
- Check syllabus for current schedule
- TAs available for assistance

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

### Templates & Documentation
- [Lab Report Template](resources/lab-resources/)
- [DE10-Lite Pin Assignments](resources/lab-resources/)
- [Grading Rubric](resources/lab-resources/)

### Setup Guides
- [AWS Cloud Setup](preparation/aws-setup/)
- [Draw.io Guide](preparation/drawio/)

### Reference Files
Located in `labs/etc/`:
- [DE10_LITE_Default.pof](etc/DE10_LITE_Default%20(1).pof) - Default configuration
- [Scratchpad.xml](etc/Scratchpad.xml) - Draw.io library
- [ECE.xml](etc/ECE.xml) - Draw.io components

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

**Ready to start? Begin with [Lab 1: Introduction to Verilog HDL](combinational/lab1)!**
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
- [DE10-Lite Pin Assignments](resources/DE10-Lite_Pins.pdf)

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
