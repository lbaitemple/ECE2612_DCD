---
layout: default
title: Assignment 0 - Setup & LED Control
parent: Assignments
nav_order: 1
---

# Assignment 0: Software Setup and LED Control
**Module 0 - Introduction**

---

## Assignment Information

- **Due Date**: End of Week 1
- **Points**: 100
- **Submission**: Canvas (PDF + Verilog files)
- **Type**: Individual
- **Estimated Time**: 4-6 hours

---

## Learning Objectives

By completing this assignment, you will:
- Install and configure FPGA development tools
- Verify proper installation of Quartus and ModelSim
- Program an FPGA board for the first time
- Implement simple combinational logic in Verilog
- Document your work professionally

---

## Prerequisites

- Computer meeting system requirements (20+ GB free space)
- DE10-Lite FPGA board (optional but recommended)
- USB cable for board connection
- Internet connection for software download

---

## Assignment Problems

### Problem 1: Software Installation and Verification (30 points)

**Part A: Installation (15 points)**

Install the following software:
1. **Intel Quartus Prime Lite Edition** (version 23.1std or later)
   - Include ModelSim-Intel FPGA Starter Edition
   - Include MAX 10 FPGA device support
2. **USB-Blaster II Driver** (included with Quartus)
3. **Draw.io** or similar diagramming tool

**Part B: Verification Screenshots (15 points)**

Take and submit screenshots showing:
1. Quartus Prime **About** dialog (Help → About) showing version number
2. ModelSim-Intel launch window showing version
3. Quartus Programmer with USB-Blaster detected (or show auto-detect screen)
4. Windows Device Manager (or Mac System Information) showing USB-Blaster driver installed

**Deliverables**:
- Four labeled screenshots in your PDF report
- Brief answers to installation questions (see rubric)

---

### Problem 2: DE10-Lite Default Configuration (20 points)

**Objective**: Program and verify the DE10-Lite default demonstration.

**Steps**:
1. Download `DE10_LITE_Default.pof` from Terasic website or course resources
2. Connect DE10-Lite board via USB
3. Open Quartus Programmer
4. Load the .pof file and program the FPGA
5. Test all peripherals on the board:
   - Toggle all 10 switches - LEDs should respond
   - Press all 4 push buttons - observe behavior
   - Verify 7-segment displays show counting pattern
   - Check accelerometer tilt demo (if applicable)

**Deliverables**:
- Photos or short video (< 30 seconds) showing:
  - Board with power LED illuminated
  - Switches controlling LEDs
  - Working 7-segment displays
  - At least one button function working
- Brief description of what each peripheral does

**Note**: If you don't have the board, you can skip this problem and complete Problem 3 in simulation only for partial credit.

---

### Problem 3: LED Logic Circuit (40 points)

**Objective**: Design and implement basic logic gates controlling LEDs.

**Requirements**:

Design a Verilog module that implements the following logic:
- **Inputs**: Three switches (SW0, SW1, SW2)
- **Outputs**: Four LEDs (LED0, LED1, LED2, LED3)

**Logic Functions**:
1. `LED0 = SW0 AND SW1`
2. `LED1 = SW0 OR SW2`  
3. `LED2 = NOT SW2`
4. `LED3 = (SW0 AND SW1) OR (NOT SW2)`

**Part A: Verilog Implementation (20 points)**

Create a Verilog module named `led_logic` that implements the above functions.

**Template**:
```verilog
module led_logic (
    input  wire SW0, SW1, SW2,
    output wire LED0, LED1, LED2, LED3
);
    // Your code here
    
endmodule
```

**Part B: Pin Assignments (10 points)**

Create pin assignments for the DE10-Lite board (or document what pins you would use):
- SW0 → PIN_C10
- SW1 → PIN_C11  
- SW2 → PIN_D12
- LED0 → PIN_A8
- LED1 → PIN_A9
- LED2 → PIN_A10
- LED3 → PIN_B10

Document how you assigned pins using either:
- Quartus Pin Planner screenshots, OR
- .qsf file excerpt, OR
- Table showing signal-to-pin mapping

**Part C: Testing and Verification (10 points)**

Create a truth table showing all 8 input combinations (2³ = 8 rows) and the expected outputs for all four LEDs.

| SW2 | SW1 | SW0 | LED3 | LED2 | LED1 | LED0 |
|-----|-----|-----|------|------|------|------|
|  0  |  0  |  0  |  ?   |  ?   |  ?   |  ?   |
|  0  |  0  |  1  |  ?   |  ?   |  ?   |  ?   |
| ... | ... | ... |  ... |  ... |  ... |  ... |

Test your circuit and verify it matches your truth table. Provide:
- Completed truth table
- Photos/video of FPGA showing at least 3 different input combinations
- OR simulation waveforms showing all 8 cases

---

### Problem 4: Reflection and Documentation (10 points)

Write a brief reflection (150-250 words) addressing:

1. **Challenges**: What difficulties did you encounter during installation or programming?
2. **Solutions**: How did you overcome these challenges?
3. **Surprises**: What surprised you about FPGA development?
4. **Questions**: What questions do you have about digital design or the tools?
5. **Next Steps**: What are you most interested in learning next?

---

## Grading Rubric

### Problem 1: Software Installation (30 points)

| Criteria | Excellent (100%) | Good (85%) | Satisfactory (70%) | Needs Improvement (50%) | Incomplete (0%) |
|----------|------------------|------------|-------------------|------------------------|----------------|
| **Installation** (15pts) | All software installed correctly, all components present | Minor component missing or old version | Missing one major component | Multiple missing components | No installation attempted |
| **Screenshots** (10pts) | All 4 required screenshots clear and properly labeled | 3 screenshots or minor quality issues | 2 screenshots or unclear labels | 1 screenshot only | No screenshots |
| **Questions** (5pts) | All questions answered thoroughly | Most questions answered | Some questions answered | Minimal responses | No responses |

**Installation Questions** (answer in PDF):
1. What version of Quartus Prime did you install?
2. What is the exact part number of the FPGA on the DE10-Lite?
3. How much disk space does your Quartus installation use?
4. Did you encounter any errors during installation? How did you resolve them?

---

### Problem 2: Default Configuration (20 points)

| Criteria | Excellent (100%) | Good (85%) | Satisfactory (70%) | Needs Improvement (50%) | Incomplete (0%) |
|----------|------------------|------------|-------------------|------------------------|----------------|
| **Programming** (10pts) | Board successfully programmed, all features work | Board programmed, minor features not working | Programming successful but limited testing | Programming partially successful | Not attempted |
| **Documentation** (10pts) | Clear photos/video of all required features | Most features documented | Some features documented | Minimal documentation | No documentation |

**Alternative (Simulation Only - 14 points max)**:
- Screenshot of successful Quartus compilation (7 pts)
- RTL viewer screenshot showing your design (7 pts)

---

### Problem 3: LED Logic Circuit (40 points)

| Criteria | Excellent (100%) | Good (85%) | Satisfactory (70%) | Needs Improvement (50%) | Incomplete (0%) |
|----------|------------------|------------|-------------------|------------------------|----------------|
| **Verilog Code** (20pts) | All logic correct, clean code, well-commented | Minor logic error or style issues | Multiple logic errors or poor style | Significant errors, compiles with warnings | Does not compile |
| **Pin Assignments** (10pts) | Correct pin assignments, properly documented | Minor pin errors or documentation issues | Missing some pins or poor documentation | Significant pin assignment errors | No pin assignments |
| **Testing** (10pts) | Complete truth table, all cases tested and verified | Minor testing gaps | Incomplete testing | Minimal testing | No testing |

**Code Quality Guidelines**:
- Use meaningful signal names
- Include module header comment
- Indent properly
- Use continuous assignments (`assign`) for combinational logic
- No syntax errors or warnings

**Example Header Comment**:
```verilog
//==============================================================================
// Module: led_logic
// Description: Implements basic logic gates using switches and LEDs
// Author: [Your Name]
// Date: [Date]
//==============================================================================
```

---

### Problem 4: Reflection (10 points)

| Criteria | Excellent (100%) | Good (85%) | Satisfactory (70%) | Needs Improvement (50%) | Incomplete (0%) |
|----------|------------------|------------|-------------------|------------------------|----------------|
| **Content** (6pts) | Thoughtful, detailed responses to all prompts | Good responses, minor gaps | Adequate but superficial | Minimal effort | No reflection |
| **Writing** (4pts) | Clear, professional, correct length | Minor writing issues | Some clarity issues or wrong length | Poor writing quality | Not submitted |

**Length Requirement**: 150-250 words (not including headers)

---

## Submission Requirements

### File Format

Submit a **single PDF** file containing:

1. **Cover Page** with:
   - Your name and student ID
   - Course name and section
   - Assignment title
   - Date submitted

2. **Problem 1**: 
   - Screenshots
   - Answers to installation questions

3. **Problem 2**:
   - Photos/video links
   - Feature descriptions

4. **Problem 3**:
   - Verilog code (formatted, not screenshot)
   - Pin assignment documentation
   - Truth table
   - Test results (photos or waveforms)

5. **Problem 4**:
   - Reflection (150-250 words)

6. **Appendix** (if needed):
   - Full .qsf file
   - Compilation reports
   - Additional notes

### Separate Verilog Files

Also upload your `.v` files separately:
- `led_logic.v`
- Any testbench files (optional for this assignment)

### File Naming

- PDF: `LastName_FirstName_Assignment0.pdf`
- Verilog: `led_logic.v`

---

## Common Issues and Solutions

### Installation Issues

**❌ Problem**: "Not enough disk space"
**✅ Solution**: 
- Quartus requires 20+ GB
- Free up space or install to different drive
- Consider external drive if needed

**❌ Problem**: "Installation failed at 80%"
**✅ Solution**:
- Disable antivirus temporarily
- Run installer as Administrator (Windows)
- Check install logs in temp directory

**❌ Problem**: "USB-Blaster driver won't install"
**✅ Solution**:
- Manually install from `quartus/drivers/usb-blaster`
- Try different USB port (prefer USB 2.0)
- On Windows: Update driver through Device Manager

### Board Connection Issues

**❌ Problem**: "Device not found in Programmer"
**✅ Solution**:
1. Verify power LED is on
2. Check USB cable (must be data cable, not charge-only)
3. Click "Auto Detect" button
4. Try different USB port
5. Restart Quartus and reconnect

**❌ Problem**: "LEDs don't respond to switches"
**✅ Solution**:
- Verify pin assignments match board schematic
- Check signal names match in Verilog and pin assignments
- Ensure you programmed successfully (check success message)
- Try reprogramming

### Verilog Compilation Issues

**❌ Problem**: "Error: Verilog syntax error"
**✅ Solution**:
- Check for missing semicolons
- Verify parentheses are balanced
- Ensure `endmodule` is present
- Check that signal names match port declarations

**❌ Problem**: "Warning: Inferred latch"
**✅ Solution**:
- Use `assign` statements for combinational logic
- Avoid using `always` blocks for this assignment
- Make sure all outputs are assigned in all cases

---

## Resources

### Software Downloads
- [Intel Quartus Prime Lite](https://www.intel.com/content/www/us/en/software-kit/785086/)
- [DE10-Lite Resources](https://www.terasic.com.tw/cgi-bin/page/archive.pl?No=1021)

### Documentation
- [DE10-Lite User Manual](http://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=1021)
- [Quartus Prime Introduction](https://www.intel.com/content/www/us/en/docs/programmable/683349/)
- [Basic Verilog Tutorial](http://www.asic-world.com/verilog/verilog_one_day.html)

### Video Tutorials
- Installing Quartus Prime (15 min)
- DE10-Lite Board Overview (10 min)
- Your First FPGA Project (20 min)

---

## Tips for Success

1. **Start Early**: Don't wait until the last minute to install software
2. **Read Error Messages**: They usually tell you exactly what's wrong
3. **Test Incrementally**: Test each LED function separately before combining
4. **Use Comments**: Document your code as you write it
5. **Take Good Photos**: Ensure photos are well-lit and in focus
6. **Keep Notes**: Document any issues you encounter and how you solved them
7. **Ask for Help**: Use office hours if you get stuck

---

## Academic Integrity

This is an **individual assignment**. You may:
- Discuss general concepts with classmates
- Ask TAs/instructor for help
- Use course materials and recommended resources

You may NOT:
- Copy code from other students
- Share your Verilog files with others
- Submit someone else's work as your own

Violations will result in zero credit and referral to academic integrity office.

---

## Late Submission Policy

- **On time**: Full credit available
- **1 day late**: -10% penalty
- **2 days late**: -20% penalty  
- **3 days late**: -30% penalty
- **More than 3 days late**: Assignment not accepted (0 points)

Special circumstances (illness, emergencies) require documentation and must be discussed with instructor before the due date.

---

**Good luck with your first FPGA design! This is the beginning of your digital design journey.** 🚀
