# Intro Engine v0.2 - API Documentation

## Overview

**Intro Engine v0.2** is a comprehensive Scratch project designed for creating animated introductions and visual effects. This engine provides a robust set of tools for animations, transitions, effects, and interactive elements suitable for video introductions, presentations, and multimedia projects.

## Project Structure

### Main Components
- **Stage**: Primary scene with global variables and control systems
- **Intro Engine V0.2 Sprite**: Main engine containing core functionality
- **Asset System**: Extensive library of SVG graphics and audio files

## Core APIs and Functions

### 1. Animation Engine APIs

#### 1.1 Easing Functions

##### `[EASING] Quintic`
**Purpose**: Provides smooth quintic easing animation for position, size, and rotation changes.

**Parameters**:
- `speed` (number): Animation speed multiplier (higher = slower)
- `x position` (number): Target X coordinate 
- `y position` (number): Target Y coordinate
- `size` (number): Target size percentage
- `direction` (number): Target rotation direction in degrees

**Usage Example**:
```scratch
call [EASING] Quintic :: Speed: (30) X: (100) Y: (50) Size: (150) Direction: (90)
```

**Description**: 
- Uses quintic easing mathematics for smooth acceleration and deceleration
- Automatically handles transition from current state to target state
- Stores initial values in EASING list for calculations
- Implements smooth interpolation using mathematical formulas

#### 1.2 Smooth Glide System

##### `advanced smooth glide to`
**Purpose**: Provides precise smooth movement with multiple parameter control.

**Parameters**:
- `x` (number): Target X position
- `y` (number): Target Y position  
- `size` (number): Target size
- `direction` (number): Target direction/rotation
- `speed` (number): Movement speed factor

**Usage Example**:
```scratch
call advanced smooth glide to x: (200) y: (-100) size: (120) direction: (45) speed: (15)
```

**Description**:
- Continues until all parameters reach target values
- Uses incremental changes divided by speed for smooth motion
- Handles simultaneous position, size, and rotation changes
- Automatically stops when targets are reached

### 2. Visual Effects APIs

#### 2.1 Camera and Shake Effects

##### `Shake: End size`
**Purpose**: Creates camera shake effect with customizable intensity and duration.

**Parameters**:
- `End size` (number): Final size after shake effect
- `Intensity` (number): Number of shake iterations

**Usage Example**:
```scratch
call Shake: End size (100) Intensity (20)
```

**Description**:
- Applies sinusoidal movement pattern for realistic shake
- Modifies camera control list for global effect
- Returns to center position after completion
- Adjustable intensity for different impact levels

##### `Shake (.5)`
**Purpose**: Alternative shake implementation with 0.5 multiplier for subtle effects.

**Parameters**:
- `End-Size` (number): Target size after effect
- `Repeat` (number): Number of repetitions

**Usage Example**:
```scratch
call Shake (.5) | (90) (10)
```

**Description**:
- Uses timer-based sinusoidal calculations
- Applies 0.5 multiplier for gentler movement
- Updates camera control in real-time
- Smooth size transitions during shake

#### 2.2 FX System

##### `FX:: Costume Start: End:`
**Purpose**: Animates through a sequence of costume frames for visual effects.

**Parameters**:
- `Start Cos. #` (number): Starting costume number
- `End Cos. #` (number): Ending costume number  
- `Dur.` (number): Duration per frame (seconds)

**Usage Example**:
```scratch
call FX:: Costume Start: (1) End: (20) Duration (0.1)
```

**Description**:
- Cycles through costume numbers sequentially
- Special handling for costume #312 with instant transitions
- Configurable frame duration for different effect speeds
- Supports both forward and reverse animations

### 3. Sprite Management APIs

#### 3.1 Clone System

##### Clone Types and Initialization
The engine supports multiple clone types with specific behaviors:

**Chevron Clones**:
- `Clone ID = "Chevron"`: Primary chevron animations
- `Clone ID = "Chevron2"`: Secondary chevron animations  
- `Clone ID = "Bars"`: Bar/transition elements

##### `Reset::`
**Purpose**: Universal sprite reset and positioning function.

**Parameters**:
- `X` (number): X position
- `Y` (number): Y position
- `Size` (number): Size percentage
- `Hide?` (string): "y" to hide, anything else to show
- `Direction` (number): Rotation direction in degrees

**Usage Example**:
```scratch
call Reset:: X: (0) Y: (0) Size: (100) Hide? (n) Direction: (90)
```

**Description**:
- Initializes sprite to specified state
- Handles visibility control
- Sets initial transformation parameters
- Used by clone initialization routines

## Variables and Data Structures

### Global Variables (Stage)

| Variable | Type | Purpose | Default |
|----------|------|---------|---------|
| `i` | Number | Iterator/counter variable | 51 |
| `Shake` | Number | Shake effect intensity | -12 |
| `count` | Number | Animation frame counter | 1 |
| `Easing Y` | String | Y-axis easing value | "0" |
| `Easing Size` | String | Size easing value | "100" |
| `Dir` | Number | Direction value | 40 |
| `RotateSpin` | Number | Rotation spin value | 0 |
| `Time Start intro` | String | Intro start time | "7.50" |
| `Time End Intro` | String | Intro end time | "15.71" |
| `Easing` | Number | General easing value | -15 |
| `Time` | String | Current time value | "5" |
| `Size` | String | Current size value | "100" |

### Lists (Data Arrays)

#### `Spline x` and `Spline y`
**Purpose**: Store coordinate points for spline-based animations.
- Contains 50 coordinate points each
- Used for complex curved motion paths
- Support smooth interpolation between points

#### `EASING`
**Purpose**: Temporary storage for easing calculations.
- Stores initial transformation values
- Used by quintic easing functions
- Format: [x, y, size, direction]

#### `Camera Control`
**Purpose**: Global camera transformation data.
- Index 1: Camera X offset
- Index 2: Camera Y offset  
- Index 3: Camera rotation/scale

#### `FX Data`
**Purpose**: Effect system configuration.
- Stores effect parameters and states
- Used by costume animation system
- Format: [state, mode, param1, param2, param3]

### Sprite Variables

#### Intro Engine V0.2 Sprite Variables

| Variable | Purpose | Type |
|----------|---------|------|
| `____(For this sprite only) Chev size` | Chevron size tracking | Number |
| `Clone ID` | Identifies clone type/behavior | String |

## Costume System

### Main Sprite Costumes

The engine includes an extensive costume library organized by categories:

#### Core Costumes
- `Null`: Transparent/empty costume
- `FG//flash`: Foreground flash effect
- `Bold lines`: Bold line graphics
- `Size Hack`: Size manipulation costume
- `Chevron`, `Chevron2`: Directional indicators
- `Bars`: Transition bar elements

#### FX Categories

##### Flare Effects (`flare//1` to `flare//24`)
- Light flare and glow effects
- Various sizes and intensities
- Suitable for impact moments

##### Ring Effects (`FX//R1` to `FX//R4`)  
- Circular expanding effects
- Ring animations
- Radial transitions

##### Animation Sequences (`FX//A1` to `FX//A20`)
- 20-frame animation sequences
- Smooth transitional effects
- Loop-compatible animations

##### Burst Effects (`FX//B1` to `FX//B20`)
- Explosive/burst animations
- Energy release effects
- Impact visualizations

##### Complex Effects (`FX//C1` to `FX//C20`)
- Advanced composite effects
- Multi-layered animations
- Complex visual transitions

##### Detail Effects (`FX//D1` to `FX//D20`)
- Fine detail animations
- Particle-like effects
- Subtle visual enhancements

##### Energy Effects (`FX//E1` to `FX//E20`)
- Energy beam effects
- Power-up animations
- Electrical/energy visuals

And continues through categories F, G, H, I, J, K, L, M with various specialized effects...

#### ShockWave Sequences
- `ShockWaveV13//1` through `ShockWaveV13//312`: 
- Comprehensive shockwave animation
- 312 total frames for extended effects
- High-resolution wave propagation

## Audio System

### Sound Assets
- `pop.wav`: UI interaction sound (44.1kHz, 1032 samples)
- Various audio effects embedded in SVG assets
- Support for multiple audio formats

## Usage Examples

### Basic Animation Setup
```scratch
// Initialize sprite
call Reset:: X: (0) Y: (0) Size: (100) Hide? (n) Direction: (90)

// Apply smooth movement
call advanced smooth glide to x: (200) y: (100) size: (150) direction: (45) speed: (20)

// Add shake effect
call Shake: End size (120) Intensity (15)
```

### Complex Effect Sequence
```scratch
// Start with flash effect
switch costume to (FG//flash)

// Apply easing animation  
call [EASING] Quintic :: Speed: (25) X: (100) Y: (-50) Size: (200) Direction: (180)

// Add costume animation effect
call FX:: Costume Start: (1) End: (20) Duration (0.08)

// Finish with gentle shake
call Shake (.5) | (100) (8)
```

### Clone-Based Effects
```scratch
// Create chevron effect
set [Clone ID] to (Chevron)
create clone of (myself)

// Create bar transition
set [Clone ID] to (Bars) 
create clone of (myself)

// Initialize clones automatically handle their specific behaviors
```

## Performance Considerations

### Optimization Guidelines

1. **Costume Management**: 
   - Use appropriate costume categories for effects
   - Avoid rapid costume switching in tight loops

2. **Animation Timing**:
   - Balance speed parameters for smooth performance
   - Use appropriate frame rates for different effects

3. **Clone Limits**:
   - Monitor active clone count
   - Clean up clones when effects complete

4. **Memory Usage**:
   - Large number of high-resolution SVG assets
   - Consider asset loading strategies for complex projects

## Integration Guide

### Adding Custom Effects

1. **Extend FX System**:
   - Add new costume sequences following naming convention
   - Implement corresponding FX calls

2. **Custom Easing**:
   - Modify EASING list structure for new parameters  
   - Implement custom mathematical functions

3. **Audio Integration**:
   - Add new sound assets to project
   - Trigger audio events with visual effects

### Event Handling

The engine responds to these key events:
- `when flag clicked`: Initializes global state
- `when I start as a clone`: Handles clone-specific behavior
- `when timer > [value]`: Time-based triggers

## Error Handling

### Common Issues

1. **Costume Not Found**: Ensure costume names match exactly
2. **Clone Behavior**: Verify Clone ID is set before creating clones  
3. **Animation Conflicts**: Avoid multiple simultaneous animations on same sprite
4. **Performance**: Monitor for excessive costume switching or clone creation

## Version History

### v0.2 Features
- Enhanced easing system with quintic curves
- Expanded FX costume library (300+ effects)
- Improved shake algorithms
- Advanced clone management
- Comprehensive spline support
- Extended audio capabilities

## License and Credits

**Project**: Intro Engine v0.2
**Platform**: Scratch 3.0
**File Format**: .sb3 (Scratch Project)
**Download**: Available via MediaFire link in README

This documentation covers the complete public API surface of the Intro Engine v0.2 project. For additional implementation details, refer to the project's block code structure and costume assets.