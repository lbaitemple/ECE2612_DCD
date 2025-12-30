---
layout: default
title: Course Modules
nav_order: 4
permalink: /docs/modules/
has_children: true
---

# Course Modules

This course consists of **12 comprehensive modules** covering digital circuit design from fundamentals through advanced topics.

---

## Module Organization

Each module includes:
- **Learning Objectives**: What you'll master
- **Topics**: Detailed content coverage
- **Examples**: Worked problems and code
- **Assignments**: Hands-on practice
- **Resources**: Additional references

---

## Module List

### Foundation (Weeks 1-5)

#### [Module 0: Course Introduction & Software Setup](module-00/)
**Week 1** | Get started with FPGA tools and your first digital circuit
- Quartus installation and configuration
- DE10-Lite board setup
- First FPGA project: LED control
- Digital design workflow

#### [Module 1: Digital Logic Fundamentals](module-01/)
**Weeks 1-2** | Master the basics of digital logic
- Number systems (binary, hex, decimal)
- Boolean algebra and logic gates
- Truth tables and logic expressions
- Circuit implementation

#### [Module 2: Combinational Logic Design](module-02/)
**Weeks 2-3** | Build complex combinational circuits
- Karnaugh maps for minimization
- Multiplexers and demultiplexers
- Decoders and encoders
- Adders and comparators

#### [Module 3: Verilog HDL Basics](module-03/)
**Week 4** | Learn hardware description language
- Verilog syntax and structure
- Dataflow and behavioral modeling
- Testbench design
- Simulation and debugging

#### [Module 4: Number Systems & Binary Representation](module-04/)
**Week 5** | Deep dive into number representations
- Signed number formats
- 2's complement arithmetic
- BCD encoding
- Fixed-point representations

---

### Intermediate (Weeks 6-10)

#### [Module 5: Binary Arithmetic & ALU Design](module-05/)
**Week 6** | Design arithmetic circuits
- Addition and subtraction
- Multiplication and division
- Overflow detection
- Complete ALU implementation

#### [Module 6: Latches and Flip-Flops](module-06/)
**Weeks 7-8** | Introduction to sequential logic
- SR, D, JK, and T flip-flops
- Timing parameters (setup, hold, propagation)
- Register design
- Synchronous vs asynchronous

#### [Module 7: Sequential Circuit Design](module-07/)
**Weeks 8-9** | Analyze and synthesize sequential circuits
- Sequential circuit analysis
- State diagrams and state tables
- Moore vs Mealy machines
- Circuit synthesis from specifications

#### [Module 8: Counters, Shift Registers, and Timers](module-08/)
**Week 10** | Build specialized sequential circuits
- Binary and BCD counters
- Up/down counters with load
- Shift registers (SISO, SIPO, PISO, PIPO)
- Timer circuits and applications

---

### Advanced (Weeks 11-14)

#### [Module 9: Finite State Machines (FSM)](module-09/)
**Weeks 11-12** | Master state machine design
- FSM design methodology
- State encoding strategies
- Datapath + control architecture
- Complex controller design

#### [Module 10: Memory Systems](module-10/)
**Week 13** | Design memory structures
- RAM and ROM implementation
- Dual-port memories
- FIFO buffers
- Cache basics

#### [Module 11: Advanced Topics](module-11/)
**Week 14** | Professional design techniques
- Clock domain crossing
- Metastability mitigation
- Pipelining for performance
- Timing closure and optimization
- Low-power design

---

## Module Navigation

Click on any module title above to access the full content. Each module page includes:

- 📖 **Lecture Notes**: Comprehensive coverage of topics
- 💻 **Code Examples**: Verilog implementations
- 🧪 **Lab Exercises**: Hands-on practice problems
- 📝 **Assignment**: Weekly graded work
- 📚 **Resources**: Additional references and links

---

## Learning Path

### Beginner Track (Modules 0-5)
Focus on fundamentals and building a solid foundation.

**Key Milestone**: Design a complete ALU

### Intermediate Track (Modules 6-8)
Master sequential logic and state machine basics.

**Key Milestone**: Implement a complex counter system

### Advanced Track (Modules 9-11)
Apply professional design techniques and optimizations.

**Key Milestone**: Complete final project

---

## Module Progression

```
Module 0: Setup
    ↓
Module 1: Boolean Algebra → Module 2: Combinational Logic
    ↓                              ↓
Module 3: Verilog HDL ←────────────┘
    ↓
Module 4: Number Systems → Module 5: Arithmetic
    ↓
Module 6: Flip-Flops → Module 7: Sequential Design
    ↓                          ↓
Module 8: Counters & Registers
    ↓
Module 9: Finite State Machines
    ↓
Module 10: Memory Systems
    ↓
Module 11: Advanced Topics
    ↓
Final Project
```

---

## Tips for Success

- **Don't skip modules**: Each builds on previous knowledge
- **Do the assignments**: Practice is essential
- **Test on hardware**: Don't rely only on simulation
- **Ask questions**: Use discussion board and office hours
- **Start early**: FPGA debugging takes time

---

## Quick Links

- [View All Assignments](../assignments/)
- [Download All Resources](../resources/)
- [Check Schedule](../syllabus/#schedule)
- [FAQ & Troubleshooting](../faq/)

---

**Ready to dive in? Start with [Module 0](module-00/)!**
