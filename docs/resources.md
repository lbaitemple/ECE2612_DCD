---
layout: default
title: Resources
nav_order: 6
permalink: /docs/resources/
---

# Course Resources

Additional learning materials, references, and tools to support your success in digital circuit design.

---

## Quick Reference

### [Verilog Quick Reference](verilog-reference/)
Essential Verilog syntax and patterns
- Data types and operators
- Always block templates
- Common design patterns
- Testbench guidelines

### [FPGA Board Reference](fpga-reference/)
DE10-Lite pin assignments and specifications
- Pin mapping table
- Clock and reset signals
- Peripheral connections
- Timing constraints

### [Boolean Algebra Cheat Sheet](boolean-algebra/)
Laws and theorems for logic minimization
- Fundamental laws
- De Morgan's theorems
- K-map rules
- Simplification examples

---

## Software Tools

### Intel Quartus Prime
- [Download Page](https://www.intel.com/content/www/us/en/software-kit/785086/)
- [User Guide](https://www.intel.com/content/www/us/en/docs/programmable/683432/)
- [Video Tutorials](https://www.intel.com/content/www/us/en/programmable/support/training/course/oqrtusw.html)
- [Keyboard Shortcuts](shortcuts/)

### ModelSim Simulator
- [User Manual](https://www.intel.com/content/www/us/en/docs/programmable/683870/)
- [Command Reference](modelsim-commands/)
- [Waveform Viewing Guide](waveform-guide/)

### Design Tools
- [Draw.io](https://app.diagrams.net/) - Block diagrams
- [WaveDrom](https://wavedrom.com/) - Timing diagrams
- [Digital](https://github.com/hneemann/Digital) - Logic simulator

---

## Online Learning

### Interactive Tutorials
- [HDLBits](https://hdlbits.01xz.net/) - Verilog practice problems
- [FPGA4Student](https://www.fpga4student.com/) - Tutorials and projects
- [Nandland](https://nandland.com/) - Verilog basics
- [EDA Playground](https://edaplayground.com/) - Online simulator

### Video Courses
- [Neso Academy](https://www.youtube.com/@nesoacademy) - Digital Electronics
- [Ben Eater](https://www.youtube.com/@BenEater) - Building 8-bit computer
- [Intel FPGA Training](https://www.intel.com/content/www/us/en/programmable/support/training/overview.html)

### Communities
- [r/FPGA](https://reddit.com/r/FPGA) - Reddit community
- [Intel Forums](https://community.intel.com/t5/Programmable-Devices/ct-p/programmable-devices)
- [EDABoard](https://www.edaboard.com/) - Electronics forum
- [Stack Overflow](https://stackoverflow.com/questions/tagged/verilog) - Verilog tag

---

## Textbooks & References

### Required Textbook
**Digital Design and Computer Architecture** by Harris & Harris
- [Publisher Page](https://www.elsevier.com/books/digital-design-and-computer-architecture/harris/978-0-12-800056-4)
- [Companion Website](http://pages.hmc.edu/harris/ddca/)
- Excellent balance of theory and practice

### Recommended Books
**Verilog HDL** by Samir Palnitkar
- Comprehensive Verilog reference
- [Online resources](http://www.asic-world.com/verilog/)

**FPGA Prototyping by Verilog Examples** by Pong P. Chu
- Hands-on FPGA projects
- Xilinx-focused but concepts apply to Intel

**Digital Design Principles and Practices** by John F. Wakerly
- Classic digital design text
- In-depth theoretical coverage

### Free Online Books
- [Free Range VHDL](https://github.com/fabriziotappero/Free-Range-VHDL-book)
- [Digital Systems](http://www.cburch.com/books/dsbook/) by Carl Burch

---

## Hardware Resources

### FPGA Boards
- [DE10-Lite](https://www.terasic.com.tw/cgi-bin/page/archive.pl?No=1021) - User manual, schematics
- [DE1-SoC](https://www.terasic.com.tw/cgi-bin/page/archive.pl?No=836) - Alternative board
- [Basys 3](https://digilent.com/shop/basys-3-artix-7-fpga-trainer-board/) - Xilinx option

### Datasheets
- [Intel MAX 10 Device Family](https://www.intel.com/content/www/us/en/docs/programmable/683794/)
- [74-series Logic ICs](https://www.ti.com/lit/ml/sdyu001ab/sdyu001ab.pdf)
- Component datasheets in `/docs/etc/datasheets/`

### Purchase Guides
- Where to buy DE10-Lite
- Component kits for breadboarding
- Tools and equipment

---

## Code Examples

### Example Projects
All examples include source code, testbenches, and documentation:

**Combinational**
- [4-bit ALU](examples/alu_4bit/)
- [Binary to BCD Converter](examples/bin2bcd/)
- [7-Segment Display Driver](examples/seven_seg/)

**Sequential**
- [Digital Clock](examples/digital_clock/)
- [UART Transmitter](examples/uart_tx/)
- [Traffic Light Controller](examples/traffic_light/)

**Advanced**
- [VGA Pattern Generator](examples/vga_patterns/)
- [Calculator](examples/calculator/)
- [Music Player](examples/music_player/)

### Templates
- [Module Template](templates/module_template.v)
- [Testbench Template](templates/testbench_template.v)
- [Makefile Template](templates/Makefile)

---

## Practice Problems

### By Module
- [Module 1 Practice](practice/module01/)
- [Module 2 Practice](practice/module02/)
- [Module 3 Practice](practice/module03/)
- ...and so on for all modules

### Problem Sets
- [Boolean Algebra Worksheet](practice/boolean_algebra.pdf)
- [K-Map Practice](practice/kmap_problems.pdf)
- [Timing Analysis Problems](practice/timing_analysis.pdf)
- [State Machine Design](practice/fsm_design.pdf)

### Solutions
- Available after assignment due dates
- Detailed explanations provided
- Multiple solution approaches shown

---

## Design Resources

### Block Diagram Templates
- [Digital System Templates](diagrams/system_templates/)
- [State Machine Diagrams](diagrams/fsm_templates/)
- [Timing Diagrams](diagrams/timing_templates/)

### Coding Standards
- [Verilog Style Guide](standards/verilog_style.md)
- [Naming Conventions](standards/naming.md)
- [Documentation Standards](standards/documentation.md)

### Best Practices
- [Design Checklist](best-practices/design_checklist.md)
- [Debugging Guide](best-practices/debugging.md)
- [Optimization Techniques](best-practices/optimization.md)

---

## Additional Materials

### Exam Resources
- [Practice Exams](exams/practice/)
- [Review Sheets](exams/review/)
- [Formula Sheets](exams/formulas/)

### Project Ideas
- [Beginner Projects](projects/beginner/)
- [Intermediate Projects](projects/intermediate/)
- [Advanced Projects](projects/advanced/)

### Career Resources
- [FPGA Engineer Career Path](career/fpga_careers.md)
- [Industry Certifications](career/certifications.md)
- [Interview Preparation](career/interviews.md)

---

## External Links

### Industry Resources
- [Intel FPGA](https://www.intel.com/content/www/us/en/products/programmable.html)
- [AMD Xilinx](https://www.xilinx.com/)
- [Lattice Semiconductor](https://www.latticesemi.com/)

### Open Source Projects
- [OpenCores](https://opencores.org/) - IP cores
- [LibreCores](https://www.librecores.org/) - Free IP
- [ZipCPU](http://zipcpu.com/) - Blog and tutorials

### News & Blogs
- [FPGA Developer](https://www.fpgadeveloper.com/)
- [All About Circuits](https://www.allaboutcircuits.com/)
- [EE Times](https://www.eetimes.com/)

---

## Course Files

### Download All Materials
- [Complete Course Package](downloads/complete_course.zip)
- [Code Examples Only](downloads/code_examples.zip)
- [Lecture Slides](downloads/lecture_slides.zip)

### Updates
Check regularly for:
- New examples and tutorials
- Updated reference materials
- Additional practice problems
- Bug fixes and errata

---

**Have a resource to suggest? Post in the discussion board or email the instructor!**
