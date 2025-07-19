# Asset Reference - Intro Engine v0.2

## Overview

The Intro Engine v0.2 contains an extensive library of visual and audio assets designed for creating professional-quality animated introductions. All visual assets are in SVG format for scalability and crisp rendering.

## Costume Categories

### Core System Costumes

#### Essential Costumes
| Costume Name | Purpose | Dimensions | Usage |
|--------------|---------|------------|--------|
| `Null` | Transparent placeholder | Minimal | Hide sprite while maintaining functionality |
| `Size Hack` | Size calculation utility | Minimal | Internal size calculations (do not use directly) |
| `Alpha` | Stage background | 255x242.5 | Stage backdrop costume |

#### User Interface Costumes
| Costume Name | Purpose | Description |
|--------------|---------|-------------|
| `FG//flash` | Foreground flash | Bright overlay effect for impact moments |
| `Bold lines` | Geometric lines | Strong linear elements for transitions |
| `Chevron` | Directional indicator | Primary arrow/chevron shape |
| `Chevron2` | Directional indicator | Secondary chevron variant |
| `Bars` | Transition bars | Horizontal bar elements for wipes |
| `Size` | Size reference | Used for size-based calculations |

### Visual Effects Library

#### Flare Effects (`flare//` series)
Professional light flare and glow effects for impact and highlights.

| Costume | Size | Intensity | Best Use Case |
|---------|------|-----------|---------------|
| `flare//1` | 180x180 | Medium | General highlights |
| `flare//5` | 240x240 | High | Major impact moments |
| `flare//24` | 152x168 | Variable | Subtle accents |
| `flare//Null` | Minimal | None | Flare system placeholder |

**Usage Guidelines**:
- Use flare//1 for standard highlight effects
- flare//5 for dramatic moments or climax points  
- flare//24 for background enhancement
- Switch to flare//Null to disable flare effects

#### Ring Effects (`FX//R` series)
Expanding circular effects perfect for burst animations and radial transitions.

| Costume | Description | Animation Style |
|---------|-------------|-----------------|
| `FX//R1` | Initial ring | Small, tight circle |
| `FX//R2` | Expanding ring | Medium expansion |
| `FX//R3` | Wide ring | Large radius |
| `FX//R4` | Final ring | Maximum expansion |

**Animation Sequence**: R1 → R2 → R3 → R4 for smooth expansion
**Reverse Sequence**: R4 → R3 → R2 → R1 for contraction

#### Animation Effects (`FX//A` series)
20-frame general-purpose animation sequences for smooth transitions.

| Range | Frames | Style | Recommended Duration |
|-------|--------|-------|---------------------|
| `FX//A1` - `FX//A5` | 1-5 | Opening | 0.15s per frame |
| `FX//A6` - `FX//A10` | 6-10 | Building | 0.12s per frame |
| `FX//A11` - `FX//A15` | 11-15 | Peak | 0.10s per frame |
| `FX//A16` - `FX//A20` | 16-20 | Closing | 0.08s per frame |

**Usage Example**:
```scratch
call FX:: Costume Start: (1) End: (20) Duration (0.12)
```

#### Burst Effects (`FX//B` series)
Explosive and energy release effects for high-impact moments.

| Range | Visual Style | Energy Level | Typical Use |
|-------|--------------|--------------|-------------|
| `FX//B1` - `FX//B5` | Initial burst | Building | Power-up start |
| `FX//B6` - `FX//B10` | Mid explosion | Medium | Impact moments |
| `FX//B11` - `FX//B15` | Peak burst | High | Climax effects |
| `FX//B16` - `FX//B20` | Dissipation | Fading | Cool-down |

**Color Coordination**: These effects work well with:
- Orange/red themes for fire effects
- Blue/white for energy effects  
- Purple for magical effects

#### Complex Effects (`FX//C` series)
Advanced composite effects with multiple visual elements.

| Range | Complexity | Elements | Performance Impact |
|-------|------------|----------|-------------------|
| `FX//C1` - `FX//C5` | Moderate | 2-3 layers | Low |
| `FX//C6` - `FX//C10` | High | 3-4 layers | Medium |
| `FX//C11` - `FX//C15` | Very high | 4-5 layers | Medium-High |
| `FX//C16` - `FX//C20` | Maximum | 5+ layers | High |

**Performance Notes**: 
- Use lower range (C1-C5) for mobile compatibility
- Reserve C16-C20 for desktop projects
- Consider frame rate when using complex effects

#### Detail Effects (`FX//D` series)
Fine particle and detail animations for subtle enhancement.

| Range | Detail Level | Best For | Layering |
|-------|--------------|----------|----------|
| `FX//D1` - `FX//D5` | Fine particles | Background ambiance | Back layer |
| `FX//D6` - `FX//D10` | Medium details | Mid-level accents | Mid layer |
| `FX//D11` - `FX//D15` | Rich details | Foreground elements | Front layer |
| `FX//D16` - `FX//D20` | Maximum detail | Hero moments | Top layer |

#### Energy Effects (`FX//E` series)
Electrical, beam, and energy-based visual effects.

| Costume | Energy Type | Appearance | Usage Context |
|---------|-------------|------------|---------------|
| `FX//E1` - `FX//E5` | Electrical | Lightning-style | Power themes |
| `FX//E6` - `FX//E10` | Beam | Laser/light rays | Sci-fi themes |
| `FX//E11` - `FX//E15` | Plasma | Flowing energy | Magic themes |
| `FX//E16` - `FX//E20` | Surge | Power waves | Technology themes |

### Extended Effect Categories

The engine includes additional effect categories F through M, each containing 20 specialized costumes:

#### Categories F-M Overview
| Category | Range | Specialization | Total Costumes |
|----------|-------|----------------|----------------|
| F | FX//F1 - FX//F20 | Fluid effects | 20 |
| G | FX//G1 - FX//G20 | Geometric patterns | 20 |
| H | FX//H1 - FX//H20 | Holographic effects | 20 |
| I | FX//I1 - FX//I20 | Impact effects | 20 |
| J | FX//J1 - FX//J20 | Jet/stream effects | 20 |
| K | FX//K1 - FX//K20 | Kinetic effects | 20 |
| L | FX//L1 - FX//L20 | Light effects | 20 |
| M | FX//M1 - FX//M20 | Motion blur effects | 20 |

### ShockWave Sequence

#### Comprehensive Animation System
The crown jewel of the effect library is the ShockWave sequence:

| Range | Frames | Description |
|-------|--------|-------------|
| `ShockWaveV13//1` - `ShockWaveV13//50` | 1-50 | Initial wave formation |
| `ShockWaveV13//51` - `ShockWaveV13//100` | 51-100 | Wave expansion |
| `ShockWaveV13//101` - `ShockWaveV13//200` | 101-200 | Peak propagation |
| `ShockWaveV13//201` - `ShockWaveV13//300` | 201-300 | Wave dissipation |
| `ShockWaveV13//301` - `ShockWaveV13//312` | 301-312 | Final fade |

**Total Frames**: 312 (approximately 26 seconds at 0.08s per frame)

**Usage Recommendations**:
- Full sequence: Epic moments, climax effects
- Partial sequences: Quick impacts (frames 1-50)
- Custom ranges: Tailored to specific timing needs

**Performance Considerations**:
- Full sequence requires significant memory
- Consider breaking into smaller chunks for complex projects
- Test performance on target devices

## Audio Assets

### Sound Library

#### Primary Audio
| Asset | Format | Sample Rate | Duration | Usage |
|-------|--------|-------------|----------|--------|
| `pop.wav` | WAV | 44.1kHz | ~0.023s | UI interactions, clicks |

#### Embedded Audio
Many SVG assets contain embedded audio data for synchronized audio-visual effects.

### Audio Integration Guidelines

#### Timing Synchronization
```scratch
// Audio-visual sync example
play sound [pop] until done
call FX:: Costume Start: (1) End: (10) Duration (0.1)
```

#### Volume Management
- UI sounds: 30-50% volume
- Effect sounds: 70-90% volume  
- Background music: 20-40% volume

## Asset Organization

### File Naming Conventions

#### Visual Assets
- **Core**: Simple descriptive names (`Null`, `Bars`, `Chevron`)
- **Effects**: Category//Type/Number (`FX//A1`, `FX//B15`)
- **Flares**: `flare//` prefix with number or descriptor
- **Shockwave**: `ShockWaveV13//` with frame number

#### Audio Assets
- Descriptive names with file extension (`pop.wav`)
- Embedded audio uses hash identifiers

### Asset Categories by Usage

#### Performance Tiers
| Tier | Complexity | Recommended Use | Frame Rate Impact |
|------|------------|-----------------|-------------------|
| Essential | Low | Always available | Minimal |
| Standard | Medium | Regular use | Low |
| Advanced | High | Special moments | Medium |
| Premium | Very High | Climax/hero shots | High |

#### Memory Usage Guide
| Asset Type | Memory Impact | Loading Strategy |
|------------|---------------|------------------|
| Core costumes | Minimal | Pre-load |
| A/B/C series | Low-Medium | Load on demand |
| D/E+ series | Medium-High | Selective loading |
| ShockWave | High | Stream if possible |

## Usage Recommendations

### Project Planning

#### Asset Selection Strategy
1. **Identify Core Needs**: Which basic effects are required?
2. **Choose Effect Categories**: Select 2-3 main FX categories
3. **Plan Sequences**: Map costume ranges to timeline
4. **Test Performance**: Verify smooth playback on target devices

#### Optimization Guidelines

##### Costume Management
```scratch
// Efficient costume switching
switch costume to [FX//A1]
wait (0.1) seconds
next costume // More efficient than specific switching
```

##### Memory Optimization
```scratch
// Strategic costume loading
if <(effect_needed) = [burst]> then
    switch costume to [FX//B1]
else
    if <(effect_needed) = [detail]> then
        switch costume to [FX//D1]
```

### Creative Guidelines

#### Color Theming
Each effect category works best with specific color schemes:
- **A series**: Universal - works with any theme
- **B series**: Warm colors (red, orange, yellow)
- **C series**: Cool colors (blue, purple, cyan)
- **D series**: Neutral tones for subtlety
- **E series**: Bright, saturated colors

#### Layering Strategy
1. **Background**: D series, subtle effects
2. **Midground**: A/B series, main action
3. **Foreground**: C/E series, accent effects
4. **Overlay**: Flares, UI elements

#### Timing Patterns
- **Quick impacts**: 0.05-0.08s per frame
- **Standard effects**: 0.1-0.15s per frame  
- **Slow builds**: 0.2-0.3s per frame
- **Dramatic moments**: 0.08-0.12s per frame

### Asset Quality Standards

#### Visual Specifications
- **Format**: SVG (vector-based)
- **Color Depth**: Full color with alpha transparency
- **Resolution**: Scalable vector graphics
- **Optimization**: Minimal file sizes while maintaining quality

#### Performance Benchmarks
- **Target FPS**: 30 FPS minimum
- **Maximum Costumes**: ~50 active per scene
- **Memory Limit**: <100MB total asset usage
- **Load Time**: <2 seconds for full effect library

This comprehensive asset reference enables informed decision-making for creating professional-quality animated introductions with the Intro Engine v0.2.