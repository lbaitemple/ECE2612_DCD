---
layout: default
title: Preparation
nav_order: 3
permalink: /docs/preparation/
has_children: true
---

# Getting Started - Course Preparation

Welcome to Digital Circuit Design! This section will help you set up your development environment and get ready for the course.

---

## Quick Start Checklist

- [ ] Install Intel Quartus Prime Lite Edition
- [ ] Install ModelSim simulator
- [ ] Set up DE10-Lite FPGA board (or configure simulation)
- [ ] Create Draw.io account
- [ ] Download course materials
- [ ] Test first FPGA project

---

## Computer Requirements

### Minimum Specifications
- **Operating System**: Windows 10/11, Linux, or macOS (with VM)
- **RAM**: 8 GB minimum (16 GB recommended)
- **Storage**: 20 GB free space for software
- **USB Port**: For FPGA board programming
- **Internet**: For software downloads and updates

### Recommended Setup
- **RAM**: 16 GB or more
- **Processor**: Intel Core i5/i7 or AMD equivalent
- **Storage**: SSD for faster compilation
- **Display**: 1920x1080 or higher

---

## Software Installation

### 1. Intel Quartus Prime Lite Edition

**Download**: [Intel FPGA Software](https://www.intel.com/content/www/us/en/software-kit/785086/)

**Version**: 23.1std or later

**Components to Install**:
- ✅ Quartus Prime (Lite Edition)
- ✅ ModelSim - Intel FPGA Starter Edition
- ✅ MAX 10 device support
- ✅ Cyclone V device support (optional)

**Installation Steps**:
1. Download installer (~6 GB)
2. Run as administrator
3. Accept license agreement
4. Select installation directory (ensure sufficient space)
5. Choose components listed above
6. Wait 30-90 minutes for installation
7. Verify installation:
   - Launch Quartus Prime
   - Check Help → About for version
   - Confirm ModelSim is accessible

**Installation Guide**: [Detailed Instructions](software-setup)

---

### 2. Drawing Tools

**Option 1: Draw.io (Recommended)**
- Web-based: [https://app.diagrams.net/](https://app.diagrams.net/)
- Desktop: [Download](https://www.drawio.com/)
- Free, no account required for basic use

**Option 2: Lucidchart**
- Web-based: [https://www.lucidchart.com/](https://www.lucidchart.com/)
- Free tier available with student account

**Template Files**:
- Download [Scratchpad.xml](../etc/Scratchpad.xml)
- Download [ECE.xml](../etc/ECE.xml)

---

### 3. Text Editor / IDE

**Recommended: Visual Studio Code**
- Download: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Install extensions:
  - Verilog-HDL/SystemVerilog
  - Wavetrace (for waveform viewing)

**Alternatives**:
- Sublime Text
- Notepad++ (Windows)
- Vim/Emacs (for advanced users)

---

## FPGA Board Setup

### DE10-Lite Board

**Purchase**: [Terasic](https://www.terasic.com.tw) (~$85-100)

**What's Included**:
- DE10-Lite board with Intel MAX 10 FPGA
- USB cable
- Quick start guide

**Board Features**:
- 50,000 logic elements
- 10 switches, 10 LEDs
- 2 push buttons
- 6 seven-segment displays
- 50 MHz clock
- VGA, accelerometer, and more

**Setup Steps**:
1. Unbox and inspect board
2. Connect USB cable to computer
3. Install USB-Blaster drivers (auto-install on Windows)
4. Program default configuration to test
5. Verify LEDs and displays work

**Setup Guide**: [Board Configuration](board-setup)

---

### Simulation-Only Option

Don't have an FPGA board yet? No problem!

You can complete most assignments using:
- ModelSim simulation
- Online simulators (EDA Playground)
- Virtual FPGA environments

**Note**: Physical board highly recommended for full learning experience.

---

## Account Setup

### 1. GitHub Account
- Create account: [github.com](https://github.com)
- Useful for version control
- Access to course repository

### 2. EDA Playground (Optional)
- Online Verilog simulator
- Sign up: [edaplayground.com](https://edaplayground.com/)
- Great for quick testing

### 3. Course Tools
- Canvas account (via university)
- Google Drive or OneDrive for backups
- Course discussion forum access

---

## Download Course Materials

### Essential Files

1. **DE10-Lite Resources**:
   - [User Manual](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=218&No=1021&PartNo=4)
   - [Default Configuration File](../etc/DE10_LITE_Default.pof)
   - [Pin Assignment Reference](../etc/DE10-Lite_pinout.pdf)

2. **Example Projects**:
   - [LED Blinker](../examples/led_blinker.zip)
   - [7-Segment Display](../examples/seven_segment.zip)
   - [Switch Control](../examples/switch_led.zip)

3. **Reference Documents**:
   - [Verilog Quick Reference](../resources/verilog_reference.pdf)
   - [Quartus Shortcuts](../resources/quartus_shortcuts.pdf)
   - [Debugging Guide](../resources/debugging_guide.pdf)

---

## Verification

### Test Your Setup

**1. Quartus Installation**
```
Start Menu → Intel FPGA → Quartus Prime Lite Edition
Help → About → Verify version 23.1 or later
```

**2. ModelSim Installation**
```
Tools → Options → EDA Tool Options
Verify ModelSim-Altera path is set
```

**3. USB-Blaster**
```
Tools → Programmer
Hardware Setup → Should show USB-Blaster
```

**4. First Project**
- Follow Module 0 instructions
- Create simple LED control circuit
- Compile and program to board
- Verify switch controls LED

---

## Troubleshooting

### Common Installation Issues

**Problem**: "Not enough disk space"  
**Solution**: Free up 20+ GB or choose different drive

**Problem**: "Installation failed at 80%"  
**Solution**: Disable antivirus, run as administrator, restart

**Problem**: "USB-Blaster not detected"  
**Solution**: 
- Check USB cable (must be data cable)
- Try different USB port
- Reinstall drivers
- Restart computer

### Getting Help

1. Check [FAQ page](../faq/)
2. Search course discussion board
3. Post question on Canvas
4. Attend office hours
5. Email instructor

---

## Next Steps

Once you've completed the setup:

1. ✅ Read the [Course Syllabus](../syllabus/)
2. ✅ Review [Module 0: Introduction](../modules/module-00/)
3. ✅ Complete Assignment 0
4. ✅ Join course communication channels
5. ✅ Mark important dates on calendar

---

## Additional Resources

- [Intel Quartus User Guide](https://www.intel.com/content/www/us/en/docs/programmable/683432/)
- [ModelSim Tutorial](https://www.intel.com/content/www/us/en/docs/programmable/683870/)
- [DE10-Lite Resources](https://www.terasic.com.tw/cgi-bin/page/archive.pl?No=1021)
- [Verilog Tutorial](https://www.asic-world.com/verilog/)

---

**Ready to start? Head to [Module 0](../modules/module-00/)!** 🚀
