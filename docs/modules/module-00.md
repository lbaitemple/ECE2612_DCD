---
layout: default
title: Module 0 - Introduction
parent: Course Modules
nav_order: 1
permalink: /docs/modules/module-00/
---

# Module 0: Course Introduction & Software Setup
**Week 1**

---

## Overview

Welcome to Digital Circuit Design! This introductory module helps you:
- Understand course structure and expectations
- Set up your development environment  
- Get familiar with FPGA development boards
- Create your first "Hello World" digital circuit

**Duration**: 1 week  
**Prerequisites**: None

---

## Learning Objectives

By the end of this module, you will:
1. Navigate the course and access resources
2. Install and configure Intel Quartus Prime
3. Connect and program an FPGA board
4. Create your first digital circuit
5. Understand the digital design workflow

---

## Topics

### 1. Course Introduction
- What is digital circuit design?
- Course structure and success strategies
- Resources available to you

### 2. Hardware Requirements
- DE10-Lite FPGA board specifications
- Computer requirements
- Alternative options (simulation-only)

### 3. Software Installation
- Intel Quartus Prime Lite Edition
- ModelSim simulator
- Drawing tools (Draw.io)
- Text editor setup

### 4. Board Setup
- Unboxing and inspection
- Driver installation
- Programming default configuration
- Testing peripherals

### 5. First Project: LED Control
- Create new project in Quartus
- Write simple Verilog code
- Assign pins
- Compile and program FPGA
- Test on hardware

---

## Assignment 0

**Due**: End of Week 1  
**Points**: 100

### Requirements

**Part 1**: Installation Verification (30 points)
- Screenshots of Quartus, ModelSim, Programmer
- Answer setup questions

**Part 2**: Default Configuration (20 points)
- Program DE10_LITE_Default.pof
- Photo/video of working board

**Part 3**: LED Control Circuit (40 points)
Expand the LED_Switch example:
- Use switches SW0, SW1, SW2
- Control LEDs with logic: AND, OR, NOT
- Submit code, pin assignments, photos

**Part 4**: Reflection (10 points)
- What challenges did you encounter?
- What surprised you?
- Questions about digital design?

[Download Assignment Template](../../assignments/assignment-00.md)

---

## Resources

### Documentation
- [Quartus Prime User Guide](https://www.intel.com/content/www/us/en/docs/programmable/683432/)
- [Module 0 Lecture Slides](../../resources/lectures/module00_slides.pdf)

### Video Tutorials
- Quartus Installation (15 min)
- DE10-Lite Board Tour (10 min)
- Your First FPGA Project (20 min)

### Helpful Links
- [Intel FPGA Support](https://www.intel.com/content/www/us/en/support/programmable.html)
- [Terasic Resources](https://www.terasic.com.tw)
- [r/FPGA Community](https://reddit.com/r/FPGA)

---

## Common Issues

### Installation Problems
- **Not enough disk space** → Free up 20+ GB
- **Installation failed** → Disable antivirus, run as admin

### Board Connection
- **USB-Blaster not detected** → Check cable, try different port
- **Device not found** → Ensure board powered, check auto-detect

### Compilation Errors
- **Syntax error** → Check semicolons, parentheses
- **Pin assignment error** → Verify pin names match manual

---

## Next Steps

After completing Module 0, proceed to:
- **[Module 1: Digital Logic Fundamentals](module-01/)**
- Review binary number systems
- Practice AND, OR, NOT operations

---

[← Back to All Modules](../) | [Next Module →](module-01/)
