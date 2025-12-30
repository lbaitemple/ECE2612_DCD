---
layout: default
title: Assignments
nav_order: 5
permalink: /docs/assignments/
has_children: true
---

# Course Assignments

All assignments for Digital Circuit Design with detailed requirements, rubrics, and submission guidelines.

---

## Assignment Structure

Each assignment includes:
- **Learning Objectives**: What skills you'll develop
- **Detailed Problems**: Step-by-step requirements
- **Grading Rubrics**: Clear expectations and point breakdown
- **Resources**: References, tutorials, and helpful links
- **Common Issues**: Troubleshooting guide
- **Submission Guidelines**: Format and naming requirements

---

## Assignment List

### Foundation Phase

- **[Assignment 0: Setup & LED Control](assignment-00/)** - Week 1
  - Software installation and verification
  - Basic combinational logic
  - FPGA programming workflow

- **[Assignment 1: Digital Logic Fundamentals](assignment-01/)** - Week 2
  - Number system conversions
  - Boolean algebra simplification
  - Truth tables and logic circuits
  - Logic calculator implementation

- **[Assignment 2: Combinational Logic](assignment-02/)** - Week 3
  - K-map minimization
  - Multiplexers and decoders
  - 7-segment display driver
  - 4-bit ALU design

- **[Assignment 3: Verilog HDL](assignment-03/)** - Week 4
  - Verilog modeling styles
  - Testbench development
  - Priority encoder design
  - Debugging exercises

### Intermediate Phase

- **[Assignment 4: Number Systems](assignment-04/)** - Week 5
  - Signed number representations
  - Binary arithmetic operations
  - BCD conversion
  - Magnitude comparator

- **[Assignment 5: Binary Arithmetic](assignment-05/)** - Week 6
  - Adder analysis and design
  - 8-bit ALU implementation
  - Multiplier design
  - Timing analysis

- **[Assignment 6: Flip-Flops](assignment-06/)** - Weeks 7-8
  - Flip-flop conversions
  - Timing parameter analysis
  - Register design
  - Sequential circuit implementation

- **[Assignment 7: Sequential Design](assignment-07/)** - Week 9
  - Sequential circuit analysis
  - State machine design (Moore vs Mealy)
  - Sequence detector implementation
  - State optimization

### Advanced Phase

- **[Assignment 8: Counters & Registers](assignment-08/)** - Week 10
  - Up/down counter design
  - Universal shift register
  - Digital clock implementation
  - BCD counter cascading

- **[Assignment 9: Finite State Machines](assignment-09/)** - Weeks 11-12
  - Traffic light controller
  - Vending machine FSM
  - UART transmitter
  - FSM optimization

- **[Assignment 10: Memory Systems](assignment-10/)** - Week 13
  - ROM lookup tables
  - Dual-port RAM
  - FIFO buffer design
  - Memory-based applications

- **[Assignment 11: Advanced Topics](assignment-11/)** - Week 14
  - Clock domain crossing
  - Pipelined design
  - Timing optimization
  - Async FIFO (bonus)

---

## Assignment Policies

### Submission Guidelines

**Format**:
- Main submission: Single PDF file
- Include: Cover page, all problems, code (formatted text, not screenshots)
- Separate files: Verilog source files (.v)

**Naming Convention**:
```
LastName_FirstName_AssignmentX.pdf
module_name.v
```

**Canvas Submission**:
1. Upload PDF first
2. Add all .v files
3. Verify uploads before deadline
4. Check for submission confirmation

### Grading Criteria

Assignments are graded on:
- **Correctness** (50%): Does it work as specified?
- **Code Quality** (20%): Clean, readable, well-documented
- **Testing** (15%): Comprehensive verification
- **Documentation** (15%): Clear explanations, diagrams

### Late Policy

- **1 day late**: -10%
- **2 days late**: -20%
- **3 days late**: -30%
- **>3 days late**: Not accepted (0 points)

Exceptions require documentation and instructor approval before deadline.

### Collaboration Policy

**Individual Assignments** (0, 1, 3, 4, 5, 6):
- Work independently
- May discuss concepts
- Cannot share code

**Group Assignments** (2, 7, 8, 9, 10, 11):
- Work with assigned group
- One submission per group
- All members contribute
- Individual grades based on contribution

### Academic Integrity

✅ **Allowed**:
- Using course materials and textbooks
- Asking TAs/instructor for help
- Discussing general concepts
- Using online references (with citation)

❌ **Not Allowed**:
- Copying code from classmates
- Sharing solution files
- Using previous semester solutions
- Submitting others' work as your own

Violations result in **zero credit** and academic integrity referral.

---

## Assignment Tips

### Time Management
- Start early (assignments take 8-15 hours)
- Read entire assignment first
- Plan your approach before coding
- Test incrementally
- Save time for documentation

### Code Quality
- Use meaningful variable names
- Add comments explaining logic
- Follow consistent formatting
- Avoid magic numbers (use parameters)
- Test edge cases

### Testing Strategy
1. Test each module separately
2. Create comprehensive testbenches
3. Verify corner cases
4. Check timing constraints
5. Test on hardware (when applicable)

### Getting Help

**Before Asking**:
1. Read assignment carefully
2. Check FAQ and common issues
3. Review module materials
4. Try debugging yourself

**Where to Get Help**:
- Office hours (best for complex issues)
- Discussion board (quick questions)
- Lab TAs (hands-on debugging)
- Instructor email (policy questions)

**When Asking**:
- Describe what you tried
- Include error messages
- Show relevant code
- Explain your understanding

---

## Grading Timeline

- Assignments graded within **2 weeks** of submission
- Grades posted on Canvas
- Solutions released after grading complete
- Regrade requests within **1 week** of grade posting

---

## Assignment Schedule

| Week | Assignment | Module | Due Date | Points |
|------|-----------|--------|----------|--------|
| 1 | Assignment 0 | Introduction | End of Week 1 | 100 |
| 2 | Assignment 1 | Logic Fundamentals | End of Week 2 | 100 |
| 3 | Assignment 2 | Combinational Logic | End of Week 3 | 100 |
| 4 | Assignment 3 | Verilog HDL | End of Week 4 | 100 |
| 5 | Assignment 4 | Number Systems | End of Week 5 | 100 |
| 6 | Assignment 5 | Binary Arithmetic | End of Week 6 | 100 |
| 7-8 | Assignment 6 | Flip-Flops | End of Week 8 | 100 |
| 9 | Assignment 7 | Sequential Design | End of Week 9 | 100 |
| 10 | Assignment 8 | Counters/Registers | End of Week 10 | 100 |
| 11-12 | Assignment 9 | FSMs | End of Week 12 | 100 |
| 13 | Assignment 10 | Memory Systems | End of Week 13 | 100 |
| 14 | Assignment 11 | Advanced Topics | End of Week 14 | 100 |

**Total**: 1200 assignment points (35% of course grade)

---

## Resources

### General Resources
- [Course Textbook](../resources/#textbooks)
- [Verilog Quick Reference](../resources/verilog-reference/)
- [FPGA Board Reference](../resources/fpga-reference/)
- [Software Installation Guide](../preparation/)

### Assignment-Specific
Each assignment page includes:
- Relevant lecture slides
- Tutorial videos
- Practice problems
- Example code
- Debugging guides

### Tools
- Intel Quartus Prime
- ModelSim Simulator
- Draw.io (diagrams)
- WaveDrom (timing diagrams)
- Git (version control - recommended)

---

**Success in assignments leads to success in the course. Start early, test thoroughly, and ask for help when needed!**
