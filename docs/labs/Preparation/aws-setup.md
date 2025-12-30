---
layout: default
title: AWS Setup Guide
parent: Preparation
nav_order: 2.02
---

# AWS Setup Guide for Digital Circuit Design

## Overview

This guide covers:
- Set up Cloud9 development environment
- Install necessary tools (Quartus, ModelSim)
- Access remote desktop using DCV

---

## AWS Console Management

<div style="text-align:center">
<img src="images/aws_man_console.png" alt="AWS Management Console" />
<p><em>Figure: AWS Management Console</em></p>
</div>

The AWS Management Console provides:
- **Search** for services
- **Recent services** quick access
- **Account/role** information

> **Note:** The remote desktop using NICE DCV can be fragile in Firefox, Safari and Edge - please use **Google Chrome**.

Key services we'll use:
1. **Cloud9** - Virtual development instance
2. **IAM** - User management, roles, policies
3. **S3** - Simple Storage Service

---

## AWS Academy Account Setup

### If You Don't Have an Account

1. Check for an email from **AWS Academy** in your Temple email

<div style="text-align:center">
<img src="images/awsemail.png" alt="AWS Academy Email" />
<p><em>Figure: AWS Academy invitation email</em></p>
</div>

2. Follow the instructions to setup an account (this is different from your University account)
3. Download the [AWS Setup PDF Guide](../resources/AWS%20Setup%20Guide%20by%20Dr%20Li%20Bai.pdf) for detailed steps

### If You Already Have an Account

- Access the [AWS Academy Canvas Console](https://awsacademy.instructure.com/)

<div style="text-align:center">
<img src="images/awscanvas.png" alt="AWS Canvas" />
<p><em>Figure: AWS Academy Canvas Console</em></p>
</div>

- You can rename your course nickname by clicking on ⋮ on the course tile

---

## Setting Up AWS Cloud9

### Requirements for Instance Setup

> **Important:** You need to create an EC2 instance

1. Click **Create environment**

<div style="text-align:center">
<img src="images/create_cloud.png" alt="Create Cloud9" />
<p><em>Figure: Create Cloud9 environment</em></p>
</div>

2. Select **New EC2 instance**
3. Configure with these settings:

### Select EC2 Instance Type

<div style="text-align:center">
<img src="images/cloud9_instance.png" alt="Cloud9 Instance Selection" />
<p><em>Figure: Cloud9 EC2 instance type selection</em></p>
</div>

| Setting | Value |
|---------|-------|
| **Instance type** | c4.xlarge (7.5GB RAM, 4 vCPU) |
| **Platform** | Ubuntu Server 22.04 (Jammy) |
| **Connection** | Secure Shell (SSH) |

### Select Operating System

<div style="text-align:center">
<img src="images/cloud9_os.png" alt="Cloud9 OS Selection" />
<p><em>Figure: Cloud9 operating system selection</em></p>
</div>

### Create the Environment

<div style="text-align:center">
<img src="images/cloud9_create.png" alt="Cloud9 Create" />
<p><em>Figure: Create Cloud9 environment</em></p>
</div>

1. After configuring, click **Create**
2. Wait for the environment to be provisioned

### Open Cloud9

<div style="text-align:center">
<img src="images/open_create_cloud9.png" alt="Open Cloud9" />
<p><em>Figure: Open Cloud9 IDE</em></p>
</div>

1. Click **Open** to access your Cloud9 IDE
2. You can add additional Cloud9 instances by clicking "Create environment"

> **Warning:** Don't create too many instances - they all run when you start the lab and consume resources!

---

## Cloud9 IDE Overview

<div style="text-align:center">
<img src="images/cloud9_ide.png" alt="Cloud9 IDE" />
<p><em>Figure: Cloud9 IDE interface</em></p>
</div>

The Cloud9 IDE provides:
1. **User settings** - Customize fonts, background colors, etc.
2. **Terminal window** - Open new terminal tabs
3. **File editor** - Edit code files
4. **Tab management** - Open multiple files

### Useful Linux Commands

```bash
# Check Ubuntu version
lsb_release -a

# Check system architecture
uname -m

# Check disk space
df -lh

# List block devices
lsblk

# Find mount point
findmnt -n -o SOURCE /
```

---

## Install Quartus and Tools

### Run the Installation Script

In your Cloud9 terminal, run:

```bash
curl -fsSL "https://temple.short.gy/ece2613" | sudo -E bash -
```

Wait approximately **10-15 minutes** for the installation to complete.

### Reboot the System

After installation completes, reboot:

```bash
sudo reboot
```

### Verify Installation

After reconnecting, verify the setup:

```bash
uname -m
df -lh
```

---

## Access DCV (Remote Desktop)

### Open DCV from Cloud9

<div style="text-align:center">
<img src="images/dcv_access.png" alt="DCV Access" />
<p><em>Figure: DCV access from Cloud9</em></p>
</div>

1. Look at the **menu bar** in Cloud9
2. Click on **Preview** → **Preview Running Application**
3. Click the **expansion icon** to open in a new browser tab

<div style="text-align:center">
<img src="images/preview_icon.png" alt="Preview Icon" />
<p><em>Figure: Preview expansion icon</em></p>
</div>

### First-Time Setup

When the desktop loads:

<div style="text-align:center">
<img src="images/desktop.png" alt="Desktop Startup" />
<p><em>Figure: DCV desktop startup</em></p>
</div>

1. You may see a startup screen
2. Click **Allow** when prompted for permissions

<div style="text-align:center">
<img src="images/desktop_allow.png" alt="Desktop Permission" />
<p><em>Figure: Desktop permission dialog</em></p>
</div>

### Configure Display for X Window

<div style="text-align:center">
<img src="images/check_cmd.png" alt="Check Command" />
<p><em>Figure: Terminal command check</em></p>
</div>

In your Cloud9 terminal, set the DISPLAY variable:

```bash
export DISPLAY=:0
```

Test that X Window is working:

```bash
xeyes &
```

You should see the "xeyes" application appear on your DCV desktop.

<div style="text-align:center">
<img src="images/xeyes.png" alt="Xeyes Test" />
<p><em>Figure: Xeyes test application</em></p>
</div>

---

## Running Quartus

### Launch Quartus from Terminal

```bash
quartus &
```

Quartus will open in your DCV remote desktop window.

### Important Files to Know

| File Extension | Description |
|----------------|-------------|
| `*.v` or `*.sv` | Verilog/SystemVerilog source files |
| `*.qpf` | Quartus Project File |
| `*.qsf` | Quartus Settings File (pin assignments) |
| `*.sof` | SRAM Object File (for programming) |
| `*.svf` | Serial Vector Format (for submission) |

---

## Quick Reference

### Starting Your Lab Session

1. Log into [AWS Academy Canvas](https://awsacademy.instructure.com/)
2. Open your course and go to **Learner Lab**
3. Click **Start Lab** and wait for green indicator
4. Click **AWS** to open console
5. Search for **Cloud9** and open your environment
6. Access DCV for GUI applications

### Ending Your Session

1. Save all your work
2. Close the DCV window
3. The Cloud9 environment will auto-hibernate after inactivity

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| DCV not loading | Use Google Chrome browser |
| Display not working | Run `export DISPLAY=:0` |
| Quartus won't start | Check if installation completed, try `which quartus` |
| Out of disk space | Run `df -lh` to check, clean up old files |

---

## Additional Resources

- [AWS Setup Guide PDF](../resources/AWS%20Setup%20Guide%20by%20Dr%20Li%20Bai.pdf)
- [EDA Playground](https://edaplayground.com/) - Online Verilog simulator
- [DE10-Lite Documentation](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&No=1021)

---
