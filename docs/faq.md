---
layout: default
title: FAQ & Help
nav_order: 7
permalink: /docs/faq/
---

# Frequently Asked Questions

Common questions and troubleshooting guide for Digital Circuit Design.

---

## General Course Questions

### Q: Do I need to buy an FPGA board?
**A:** Highly recommended but not required. You can complete most assignments using ModelSim simulation. However, hands-on hardware experience is valuable and the board costs ~$85-100.

### Q: Can I use a different FPGA board?
**A:** Yes, but pin assignments will differ. DE10-Lite is recommended because course materials reference it directly. Contact instructor if using alternative board.

### Q: How much time should I expect to spend on this course?
**A:** Plan for 8-12 hours per week:
- 3 hours lecture
- 2-3 hours reading/studying  
- 3-4 hours assignments
- 2-3 hours labs

### Q: Can I work with a partner on assignments?
**A:** You can discuss concepts and debug together, but submitted code must be your own. Copying code violates academic integrity policy.

### Q: What programming background do I need?
**A:** Basic programming concepts (variables, loops, conditionals). Experience with C, Python, or Java is helpful but not required. Verilog is different from software programming.

---

## Software & Installation

### Q: Quartus installation is taking forever. Is this normal?
**A:** Yes! Installation can take 30-90 minutes due to large size (~6GB). Be patient and don't interrupt the process.

### Q: I'm on macOS. Can I run Quartus?
**A:** Quartus doesn't run natively on macOS. Options:
- Use Parallels/VMware with Windows VM
- Use university lab computers
- Use remote desktop to Windows machine
- Some older Quartus versions support Linux via Wine

### Q: Do I need to install all Quartus components?
**A:** Required: Quartus Prime Lite, ModelSim, MAX 10 device support. Optional but recommended: Cyclone V support, example designs.

### Q: ModelSim won't start. What should I do?
**A:** 
1. Check that path is set in Quartus (Tools → Options → EDA Tool Options)
2. Try running ModelSim standalone to verify installation
3. Ensure you have ModelSim-Intel FPGA Edition (not Altera Edition)
4. Reinstall if necessary

---

## Hardware & Board Issues

### Q: My USB-Blaster isn't being detected. Help!
**A:**
1. Check USB cable - must be data cable, not charge-only
2. Try different USB port (prefer USB 2.0 ports)
3. Reinstall drivers: Quartus/drivers/usb-blaster
4. Check Device Manager (Windows) for unknown devices
5. Restart computer

### Q: Programmer says "Device not found"
**A:**
1. Ensure board is powered (power LED should be on)
2. Click "Auto Detect" in Programmer
3. Select correct device (10M50DAF484 for DE10-Lite)
4. Check USB-Blaster connection
5. Try different USB cable/port

### Q: My circuit doesn't work on the FPGA but simulates correctly
**A:**
1. Verify pin assignments match your board's manual
2. Check for unconnected signals
3. Add reset logic
4. Look for timing violations in Timing Analyzer
5. Use SignalTap to debug on-chip

### Q: Can I damage the FPGA board?
**A:** Unlikely with normal use. The board has protection circuits. Don't:
- Apply excessive voltage to I/O pins
- Short power/ground
- Connect incompatible external devices
- Spill liquids on board

---

## Verilog & Coding

### Q: What's the difference between `=` and `<=` in Verilog?
**A:**
- `=` is blocking assignment (used in combinational always blocks)
- `<=` is non-blocking assignment (used in sequential always blocks)
- Using wrong type can cause simulation/synthesis mismatches

### Q: Why does my code simulate but not synthesize?
**A:** Common reasons:
- Using delay statements (#)
- Initial blocks (not supported for synthesis)
- Non-synthesizable constructs ($random, $display in main code)
- Incomplete sensitivity lists
- Latches from incomplete if/case statements

### Q: How do I create a testbench?
**A:** Basic template:
```verilog
`timescale 1ns/1ps
module tb_mymodule;
    reg inputs;
    wire outputs;
    
    mymodule dut (.in(inputs), .out(outputs));
    
    initial begin
        // Test cases
        inputs = 0; #10;
        inputs = 1; #10;
        $finish;
    end
endmodule
```

### Q: What's a "latch" and why is it bad?
**A:** Latch is unintended memory element from incomplete combinational logic. Avoid by:
- Always assign all outputs in all branches
- Use default case in case statements
- Initialize all variables in always blocks

---

## Assignments & Grading

### Q: How are assignments graded?
**A:** Typical breakdown:
- Correctness: 50% (works as specified)
- Code quality: 20% (readable, commented, organized)
- Testing: 15% (comprehensive testbench)
- Documentation: 15% (report, screenshots)

### Q: Can I submit assignments late?
**A:** Yes, with 10% penalty per day (max 3 days late). After that, zero credit. Plan ahead!

### Q: My code works on my computer but not when you test it
**A:** Common issues:
- Hardcoded absolute paths
- Missing files
- Platform-specific code
- Incorrect file names/structure
Submit exactly what you tested!

### Q: Can I revise and resubmit?
**A:** No revisions after grading. Make sure to test thoroughly before submission. Use office hours if you need pre-submission help.

---

## Exams

### Q: What can I bring to exams?
**A:** One 8.5"×11" handwritten note sheet (both sides), calculator (no programming features), pen/pencil.

### Q: Are exams multiple choice?
**A:** Mix of multiple choice, short answer, and design problems. See exam templates for format.

### Q: Can I use Verilog on exams?
**A:** Usually questions ask for circuits, truth tables, or pseudocode. Specific Verilog syntax not required unless specified.

### Q: What if I miss an exam?
**A:** Contact instructor immediately. Make-ups only for documented emergencies (medical, family, etc.).

---

## Project

### Q: When should I start the final project?
**A:** Start thinking about ideas by Week 8. Proposal due Week 10. Begin implementation by Week 11 at latest.

### Q: Can I work with a partner?
**A:** Usually individual projects. Ask instructor if you have a complex project idea requiring collaboration.

### Q: What makes a good project?
**A:** 
- Demonstrates multiple course concepts
- Appropriate complexity for time available
- Clear objectives and deliverables
- Personal interest/creativity

### Q: Can I use external IP cores?
**A:** Must implement major components yourself. Small utility blocks (like UART) may be allowed with citation. Ask first!

---

## Debugging Help

### Q: My design doesn't compile. Where do I start?
**A:**
1. Read error message completely
2. Check line number indicated
3. Look for: missing semicolons, unmatched parentheses, typos
4. Verify all signals declared
5. Check module ports match instantiation

### Q: Simulation shows 'X' (unknown). What does that mean?
**A:** Signal is uninitialized or has conflict. Check:
- Unconnected inputs
- Multiple drivers
- Missing reset
- Uninitialized registers

### Q: How do I debug timing violations?
**A:**
1. Run Timing Analyzer
2. Identify critical path
3. Options:
   - Pipeline long paths
   - Reduce clock frequency
   - Optimize logic
   - Add timing constraints

### Q: Where can I get help debugging?
**A:**
1. Re-read module materials
2. Check FAQ (here!)
3. Post on discussion board with:
   - Clear problem description
   - Error messages
   - What you've tried
   - Minimal code example
4. Office hours
5. Email instructor

---

## Tools & Resources

### Q: Is there a Verilog syntax highlighter for [editor]?
**A:** 
- VS Code: Install "Verilog-HDL/SystemVerilog" extension
- Sublime: Install "Sublime Verilog" package
- Vim: Built-in syntax highlighting
- Notepad++: Download Verilog UDL

### Q: Can I use VHDL instead of Verilog?
**A:** Course focuses on Verilog. VHDL knowledge transferable but assignments must use Verilog.

### Q: Are there online Verilog simulators?
**A:** Yes:
- EDA Playground (edaplayground.com)
- HDLBits (hdlbits.01xz.net) - practice problems
- FPGA4Student online simulator

### Q: Where can I practice Verilog?
**A:** 
- HDLBits - interactive problems
- Asic-World tutorials
- Course practice problems
- Previous assignments

---

## Academic Integrity

### Q: What constitutes cheating?
**A:**
- Copying code from classmates
- Sharing solution files  
- Submitting code from online sources without understanding
- Using previous semester's solutions

### Q: What collaboration is allowed?
**A:**
- Discussing concepts and approaches
- Debugging strategies (without sharing code)
- Explaining Verilog syntax
- Studying together

### Q: How do I cite external resources?
**A:** In code comments:
```verilog
// Clock divider based on approach from
// www.example.com/clock-divider-tutorial
// Modified for our requirements
```

---

## Still Have Questions?

1. **Check course materials**: Module content, lectures, resources
2. **Search discussion board**: Question may already be answered
3. **Post on discussion board**: Help others learn too!
4. **Attend office hours**: Best for detailed help
5. **Email instructor**: For private concerns

---

**Office Hours**: [Days/Times] in [Location]  
**Email**: [instructor@university.edu]  
**Discussion Board**: [Canvas link]

---

*This FAQ is updated regularly. Suggest additions via discussion board!*
