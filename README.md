# Disk Scheduling Algorithm Visualizer - Execution Guide

## 📋 Overview
This is a standalone web-based interactive tool for visualizing disk scheduling algorithms. It provides step-by-step animated demonstrations of FCFS, SSTF, SCAN, C-SCAN, LOOK, and C-LOOK algorithms with real-time statistics and analysis.

---

## Setup Instructions

### Quick Start
1. **Save the HTML file** to your computer (e.g., `disk_scheduling_visualizer.html`)
2. **Open the file** by double-clicking it, or right-click and select "Open with" → Choose your web browser
3. **Start visualizing** - The application runs entirely in your browser, no installation required!

### Alternative Methods
- **Drag and Drop**: Drag the HTML file into an open browser window
- **File Menu**: In your browser, go to File → Open File → Select the HTML file
- **Web Server**: For advanced users, serve via any HTTP server (Python, Node.js, etc.)

### No Server Required
✓ Complete client-side implementation  
✓ Zero dependencies or installations  
✓ Works offline  
✓ No configuration needed

---

## User Interface Guide

### Control Panel (Left Side)

#### 1. Algorithm Selection
- **Dropdown Menu**: Select from 6 disk scheduling algorithms:
  - **FCFS**: First Come First Serve - Processes requests in order of arrival
  - **SSTF**: Shortest Seek Time First - Selects closest request
  - **SCAN**: Elevator algorithm - Services requests in one direction, then reverses
  - **C-SCAN**: Circular SCAN - Services in one direction, jumps back to start
  - **LOOK**: Like SCAN but only goes to last request
  - **C-LOOK**: Circular LOOK - Like C-SCAN but only to last request

#### 2. Input Parameters

**Request Queue** (Required)
- Enter comma-separated cylinder numbers
- Example: `98, 183, 37, 122, 14, 124, 65, 67`
- **Limits**: Maximum 100 requests
- **Range**: Each value must be between 0 and disk size - 1
- **Validation**: Automatically filters invalid entries

**Initial Head Position** (Required)
- Starting position of the disk read/write head
- **Range**: 0 to (disk size - 1)
- **Default**: 53
- Must be less than disk size

**Disk Size** (Required)
- Total number of cylinders on the disk
- **Range**: 10 to 10,000 cylinders
- **Default**: 200
- Represents the maximum addressable position

**Initial Direction** (For SCAN/LOOK algorithms)
- **Right (Increasing)**: Head moves toward higher cylinder numbers
- **Left (Decreasing)**: Head moves toward lower cylinder numbers
- Only affects SCAN, C-SCAN, LOOK, and C-LOOK algorithms

#### 3. Action Buttons

**Start Visualization**
- Validates all inputs
- Calculates algorithm steps
- Initializes the visualization
- Shows error messages if validation fails

**Reset**
- Returns to step 0
- Stops animation
- Maintains current algorithm data

---


### Visualization Area (Right Side)

#### Canvas Display

**Disk Track Visualization**
- Horizontal line representing disk cylinders
- Tick marks show cylinder positions
- Scale adjusts based on disk size

**Request Points**
- Purple circles indicate request positions
- All requests shown on the track simultaneously

**Execution Path**
- Animated line showing head movement
- Color-coded points:
  - **Teal (🟦)**: Visited positions
  - **Red (🔴)**: Current head position (with pulsing outline)
- Dashed lines connect sequential movements

**Real-time Labels**
- **Current**: Current cylinder position
- **From**: Previous position
- **Seek**: Distance moved in current step
- **Total**: Cumulative seek distance

#### Playback Controls

**▶ Play**
- Starts automatic step-by-step animation
- Speed controlled by speed slider
- Auto-stops at end

**⏸ Pause**
- Pauses animation at current step
- Can resume with Play button

**⏮ Step Back**
- Moves one step backward
- Auto-pauses animation
- Disabled at step 0

**⏭ Step Forward**
- Advances one step forward
- Auto-pauses animation
- Disabled at last step

**Speed Control Slider**
- Range: 1x to 10x speed
- Higher values = faster animation
- Minimum delay: 100ms between steps

**Interactive Timeline**
- Progress bar shows current position
- Click anywhere to jump to that step
- Auto-pauses animation when clicked
- Purple gradient indicates progress

#### Statistics Panel

**Total Seek Distance**
- Sum of all head movements
- Measured in cylinders
- Lower is better

**Average Seek Time**
- Total distance ÷ number of requests
- Indicates algorithm efficiency
- Decimal precision for accuracy

**Current Step**
- Shows "X/Y" format
- X = current step, Y = total steps
- Updates in real-time

**Algorithm**
- Displays currently selected algorithm
- Confirms which algorithm is running

**Seek Sequence Display**
- Shows complete path in order
- Format: "53 → 65 → 67 → ..."
- Updates as animation progresses

---

## Animation Features

### Visual Elements

**Color Coding System**
- **Purple (#667eea)**: Request points, branding, active elements
- **Teal (#4ecdc4)**: Visited positions in sequence
- **Red (#ff6b6b)**: Current head position (active)
- **Dark gradient**: Background for contrast
- **White/Gray**: Labels, text, track lines

**Animation Effects**
- Smooth transitions between steps
- Pulsing outline on current position
- Dashed path lines for clarity
- Alternating height levels prevent overlap
- Fade-in effects for statistics

### Frame-by-Frame Transitions
- Each step shows one disk head movement
- Clear visual indication of direction
- Path builds progressively
- Statistics update synchronously

### Interactive Timeline
- Scrub through execution history
- Visual progress indicator
- Click-to-jump functionality
- Smooth synchronization with canvas

---

## Browser Requirements

### Minimum Browser Versions
✓ **Chrome/Edge**: Version 90+ (April 2021)  
✓ **Firefox**: Version 88+ (April 2021)  
✓ **Safari**: Version 14+ (September 2020)  
✓ **Opera**: Version 76+ (April 2021)

### Required Features
- HTML5 Canvas API support
- ES6+ JavaScript (const, let, arrow functions, template literals)
- CSS3 (Grid, Flexbox, gradients, transforms)
- FileReader API (for export functionality)
- JSON support

### Recommended Specifications
- **Screen Resolution**: 1280x720 minimum
- **RAM**: 2GB minimum
- **Processor**: Any modern CPU
- **Internet**: Not required (runs offline)

### Performance Notes
- Handles up to 100 requests smoothly
- Animations run at 60 FPS on modern hardware
- Canvas automatically scales to container
- Responsive design adapts to window size

---

## Input Validation & Safety

### Automatic Validation
The tool includes comprehensive input validation:

✓ **Empty Input Detection**: Prevents submission with no requests  
✓ **Number Validation**: Filters non-numeric entries  
✓ **Range Checking**: Ensures values are within bounds  
✓ **Duplicate Detection**: Warns about duplicate requests (non-blocking)  
✓ **Boundary Enforcement**: Clamps values to valid ranges  
✓ **Real-time Feedback**: Input fields adjust automatically

### Error Handling
- **Visual Error Messages**: Red notification boxes with specific issues
- **Console Logging**: Detailed warnings and success messages
- **Graceful Degradation**: Filters invalid data rather than crashing
- **Try-Catch Blocks**: Prevents JavaScript errors from breaking app

### Safety Limits
- **Max Requests**: 100 (prevents performance issues)
- **Max Disk Size**: 10,000 cylinders (prevents rendering issues)
- **Min Disk Size**: 10 cylinders (ensures usable visualization)
- **Speed Range**: 1-10x (prevents too-fast/too-slow animations)
- **Animation Delay**: Minimum 100ms (prevents browser lag)

---

## Understanding the Algorithms

### FCFS (First Come First Serve)
- **Strategy**: Processes requests in arrival order
- **Advantages**: Simple, fair, no starvation
- **Disadvantages**: High seek time, not optimized
- **Best For**: Light loads, sequential access patterns

### SSTF (Shortest Seek Time First)
- **Strategy**: Always moves to nearest request
- **Advantages**: Lower average seek time than FCFS
- **Disadvantages**: Can cause starvation, request ordering matters
- **Best For**: Moderate loads, clustered requests

### SCAN (Elevator Algorithm)
- **Strategy**: Services requests in one direction to end, then reverses
- **Advantages**: Prevents starvation, predictable
- **Disadvantages**: May skip nearby requests temporarily
- **Best For**: Heavy loads, uniform request distribution

### C-SCAN (Circular SCAN)
- **Strategy**: Services in one direction, jumps back to start
- **Advantages**: More uniform wait times than SCAN
- **Disadvantages**: May have longer total seek distance
- **Best For**: High-priority uniform response times

### LOOK
- **Strategy**: Like SCAN but reverses at last request (doesn't reach end)
- **Advantages**: More efficient than SCAN
- **Disadvantages**: Similar to SCAN limitations
- **Best For**: Optimized version of SCAN

### C-LOOK (Circular LOOK)
- **Strategy**: Like C-SCAN but only goes to last request
- **Advantages**: Most efficient circular algorithm
- **Disadvantages**: Complex implementation
- **Best For**: High-performance systems needing uniform response

---

## Troubleshooting

### Issue: Page doesn't load
- **Solution**: Ensure you're using a modern browser (see Browser Requirements)
- Check browser console for errors (F12 → Console tab)

### Issue: Validation errors appear
- **Solution**: Check that all requests are within 0 to disk size - 1
- Ensure initial head position < disk size
- Verify comma-separated format for requests

### Issue: Animation is too fast/slow
- **Solution**: Adjust speed slider (1-10x)
- Reset and try different speed setting

### Issue: Canvas appears blank
- **Solution**: Click "Start Visualization" after entering parameters
- Check that requests are valid numbers

### Issue: Export buttons don't work
- **Solution**: Start a visualization first
- Check browser permissions for downloads

---


## Technical Details

### Architecture
- **Modular Design**: Separate concerns (UI, algorithms, rendering)
- **State Management**: Centralized state object
- **Event-Driven**: Responsive to user interactions
- **Canvas Rendering**: Hardware-accelerated graphics

### File Structure
Single HTML file containing:
- HTML structure
- CSS styling (embedded)
- JavaScript logic (embedded)
- No external dependencies

### Data Flow
1. User inputs parameters
2. Validation checks inputs
3. Algorithm calculates steps
4. Animation renders frames
5. Statistics update in real-time

---

## Quick Reference

| Action | Shortcut/Method |
|--------|----------------|
| Start visualization | Click "Start Visualization" |
| Play/Pause | Play/Pause buttons |
| Step through | Step Forward/Back buttons |
| Jump to step | Click on timeline |
| Adjust speed | Drag speed slider |
| Capture screen | Screenshot button (📸) |
| Save data | Export button (📊) |
| Reset | Reset button |

---
