# Images Directory

This directory contains all images used in the course website, including diagrams, circuit schematics, timing diagrams, and screenshots.

## Directory Structure

```
images/
├── assignments/     # Images specific to assignment problems
├── modules/         # Images for module content and examples
├── diagrams/        # Circuit diagrams, state machines, block diagrams
└── examples/        # Code examples, simulation screenshots
```

## Image Naming Conventions

### Assignments
- Format: `assignment-XX-problemY-description.png`
- Examples:
  - `assignment-02-kmaps-example.png`
  - `assignment-09-traffic-light-fsm.png`
  - `assignment-10-fifo-diagram.png`

### Modules
- Format: `module-XX-topic-description.png`
- Examples:
  - `module-01-truth-table.png`
  - `module-06-timing-diagram.png`
  - `module-09-state-machine.png`

### Diagrams
- Format: `type-description.png`
- Examples:
  - `circuit-4bit-adder.png`
  - `fsm-sequence-detector.png`
  - `timing-setup-hold.png`

### Examples
- Format: `example-topic-description.png`
- Examples:
  - `example-verilog-testbench.png`
  - `example-modelsim-waveform.png`
  - `example-quartus-rtl.png`

## Using Images in Markdown

### Relative Path (Recommended)
```markdown
![Alt Text](../images/diagrams/circuit-4bit-adder.png)
```

### From Assignments
```markdown
![K-Map Example](../images/assignments/assignment-02-kmaps-example.png)
```

### From Modules
```markdown
![Timing Diagram](../images/modules/module-06-timing-diagram.png)
```

### With Caption
```markdown
![4-Bit Adder](../images/diagrams/circuit-4bit-adder.png)
*Figure 1: 4-bit ripple carry adder schematic*
```

### Sizing Images
```markdown
<img src="../images/diagrams/circuit-4bit-adder.png" alt="4-Bit Adder" width="600">
```

## Image Guidelines

### Technical Requirements
- **Format**: PNG preferred (lossless), JPG for photos
- **Resolution**: 
  - Diagrams: 1200-2400px width
  - Screenshots: 1920px width max
  - Icons: 512px or SVG
- **File Size**: < 500KB per image (compress if needed)
- **DPI**: 150-300 for diagrams

### Content Guidelines
- **Clarity**: High contrast, readable text
- **Labels**: All signals, components clearly labeled
- **Background**: White or transparent preferred
- **Colors**: Accessible color schemes (consider color blindness)

### Circuit Diagrams
- Use standard logic gate symbols
- Clear signal names
- Show power/ground connections when relevant
- Include pin numbers for ICs if applicable

### Timing Diagrams
- Clear clock edges
- Labeled signals
- Time scale indicated
- Setup/hold times marked

### State Machines
- Clear state bubbles
- Labeled transitions
- Output values indicated
- Reset state clearly marked

## Available Images from Canvas Export

Total images found: **223**

### Categories:
- Circuit schematics
- State machine diagrams
- Timing diagrams
- Code screenshots
- Simulation waveforms
- Exam problems/solutions
- Board images (DE10-Lite, etc.)

## Converting Canvas Images

To copy images from Canvas export:

```bash
# Copy relevant images to appropriate directories
cp canvas_export/web_resources/course_image/*.png docs/images/modules/
cp canvas_export/web_resources/Previous/Exam2-images-tables/*.png docs/images/examples/
```

## Image Optimization

### Compress PNG
```bash
# Using optipng
optipng -o7 image.png

# Using pngquant
pngquant --quality=80-95 image.png
```

### Compress JPG
```bash
# Using imagemagick
convert input.jpg -quality 85 output.jpg
```

### Convert to WebP (modern format)
```bash
cwebp -q 85 input.png -o output.webp
```

## Image Sources

### Original Content
- Hand-drawn circuit diagrams (scanned/digital)
- Custom timing diagrams
- Original FSM designs
- FPGA board photos

### Canvas Export
- Previous exam diagrams
- Example circuits
- Tutorial screenshots
- Reference images

### External Resources (with attribution)
- IC datasheets (cite manufacturer)
- Reference circuit diagrams (cite source)
- FPGA board images (cite Terasic/Intel)

## Attribution Template

For external images:
```markdown
![Description](path/to/image.png)
*Source: [Intel Corporation](https://intel.com) - Used with permission*
```

## Common Image Types

### Circuit Diagrams
- Logic gate circuits
- Flip-flop configurations
- Counter circuits
- Arithmetic circuits (adders, multipliers)
- Memory systems

### State Machines
- FSM state diagrams
- State transition tables
- Moore vs Mealy examples
- Protocol state machines

### Timing
- Setup and hold time diagrams
- Clock-to-Q timing
- Propagation delay
- Critical path analysis
- Waveform simulations

### FPGA/Hardware
- DE10-Lite board layout
- Pin assignment diagrams
- Quartus screenshots
- Programming interface

### Code Examples
- Verilog syntax highlighting
- Testbench examples
- Synthesis results
- RTL viewer output

## Tools for Creating Images

### Circuit Diagrams
- **Logisim**: Logic circuit simulation
- **CircuitVerse**: Online circuit simulator
- **Draw.io/Diagrams.net**: General diagramming
- **KiCad**: Professional EDA tool

### State Machines
- **FSM Designer**: Online FSM tool
- **Draw.io**: State diagram templates
- **PlantUML**: Text-based state diagrams

### Timing Diagrams
- **WaveDrom**: Digital timing diagram editor (JSON-based)
- **TimingAnalyzer**: Part of Quartus
- **Draw.io**: Manual timing diagrams

### Screenshots
- **macOS**: Cmd+Shift+4 (selection)
- **Windows**: Snipping Tool / Snip & Sketch
- **Linux**: Flameshot, Shutter

## Image Checklist

Before adding an image:
- [ ] Image is necessary (adds value, not decorative)
- [ ] Proper resolution and clarity
- [ ] File size optimized
- [ ] Descriptive filename
- [ ] Alt text provided in markdown
- [ ] Source attributed (if external)
- [ ] Placed in correct subdirectory
- [ ] Referenced correctly in content

## Future Enhancements

- [ ] Add LaTeX circuit diagrams (circuitikz)
- [ ] Create SVG versions for scalability
- [ ] Implement lazy loading for performance
- [ ] Add image gallery pages
- [ ] Create thumbnail versions
- [ ] Implement dark mode variants

---

**Note**: When adding new images, follow naming conventions and update this README with any new categories.
