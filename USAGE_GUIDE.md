# Usage Guide - Intro Engine v0.2

## Getting Started

### Quick Start
1. **Download**: Get the project from the MediaFire link in README.md
2. **Import**: Open the `.sb3` file in Scratch 3.0
3. **Initialize**: Click the green flag to start
4. **Customize**: Modify parameters to create your intro

### Project Setup
```scratch
when flag clicked
// Initialize global variables
set [Time Start intro] to [0]
set [Time End Intro] to [10]
reset timer
```

## Basic Tutorials

### Tutorial 1: Simple Animation Sequence

#### Goal: Create a basic sprite animation with movement and effects

```scratch
when flag clicked
// Step 1: Reset sprite to starting position
call Reset:: X: (-200) Y: (0) Size: (50) Hide? () Direction: (90)

// Step 2: Apply smooth movement
call advanced smooth glide to x: (0) y: (0) size: (100) direction: (90) speed: (20)

// Step 3: Add visual effect
call FX:: Costume Start: (1) End: (10) Duration (0.15)

// Step 4: Apply shake for impact
call Shake: End size (100) Intensity (10)
```

**Expected Result**: Sprite smoothly moves from left to center, plays effect animation, then shakes

#### Customization Options:
- **Speed**: Lower values (5-10) for fast movement, higher (30-50) for slow
- **Effects**: Try different costume ranges (1-20, 50-70, etc.)
- **Intensity**: Shake values 5-30 for different impact levels

---

### Tutorial 2: Multi-Layer Effects with Clones

#### Goal: Create layered visual effects using multiple clones

```scratch
when flag clicked
// Create background bars
set [Clone ID] to [Bars]
create clone of (myself)

wait (0.5) seconds

// Create primary chevron
set [Clone ID] to [Chevron]
create clone of (myself)

wait (0.2) seconds

// Create secondary chevron for depth
set [Clone ID] to [Chevron2]  
create clone of (myself)

// Main sprite effect
call [EASING] Quintic :: Speed: (30) X: (100) Y: (0) Size: (150) Direction: (45)
```

**Layer Sequence**:
1. Bars appear as background overlay
2. Primary chevron animates in foreground
3. Secondary chevron adds depth
4. Main sprite performs eased animation

---

### Tutorial 3: Timed Effect Sequence

#### Goal: Create a synchronized intro with precise timing

```scratch
when flag clicked
set [Time Start intro] to [0]
set [Time End Intro] to [15]
reset timer

// Phase 1: Opening (0-3 seconds)
call Reset:: X: (0) Y: (0) Size: (200) Hide? () Direction: (90)
call Shake (.5) | (150) (20)

wait until <(timer) > (3)>

// Phase 2: Main animation (3-8 seconds)  
call [EASING] Quintic :: Speed: (40) X: (150) Y: (-50) Size: (100) Direction: (180)

wait until <(timer) > (8)>

// Phase 3: Effects sequence (8-12 seconds)
call FX:: Costume Start: (1) End: (50) Duration (0.08)

wait until <(timer) > (12)>

// Phase 4: Closing (12-15 seconds)
call advanced smooth glide to x: (0) y: (200) size: (50) direction: (90) speed: (25)
```

---

## Advanced Techniques

### Custom Easing Curves

#### Creating Custom Movement Patterns
```scratch
define custom bounce to x: (target_x) y: (target_y)
    set [bounce_height] to [100]
    set [bounce_count] to [3]
    
    repeat (bounce_count)
        // Up motion
        call advanced smooth glide to x: (target_x) y: (y position + bounce_height) size: (size) direction: (direction) speed: (15)
        
        // Down motion with diminishing height
        change [bounce_height] by (-30)
        call advanced smooth glide to x: (target_x) y: (target_y) size: (size) direction: (direction) speed: (10)
```

#### Implementing Elastic Effects
```scratch
define elastic entrance from x: (start_x) to: (end_x)
    go to x: (start_x) y: (y position)
    
    // Overshoot phase
    call advanced smooth glide to x: (end_x + 50) y: (y position) size: (120) direction: (direction) speed: (20)
    
    // Settle back
    call advanced smooth glide to x: (end_x) y: (y position) size: (100) direction: (direction) speed: (30)
```

### Complex Visual Effects

#### Layered Shockwave Effect
```scratch
define create shockwave at x: (x) y: (y) intensity: (intensity)
    // Create multiple clones for layered effect
    repeat (intensity)
        set [Clone ID] to [ShockWave]
        go to x: (x) y: (y)
        create clone of (myself)
        wait (0.1) seconds
```

#### Particle Burst System
```scratch
define particle burst count: (count) spread: (spread)
    repeat (count)
        set [Clone ID] to [Particle]
        set [particle_angle] to (pick random (0) to (360))
        set [particle_speed] to (pick random (5) to (spread))
        create clone of (myself)
```

### Audio Synchronization

#### Syncing Effects to Audio Beats
```scratch
when flag clicked
// Define beat timing (in seconds)
add [2.5] to [beat_times]
add [4.1] to [beat_times]  
add [6.8] to [beat_times]
add [9.2] to [beat_times]

set [current_beat] to [1]

forever
    if <(timer) > (item (current_beat) of [beat_times])> then
        // Trigger effect on beat
        call Shake: End size (100) Intensity (15)
        change [current_beat] by (1)
        
        if <(current_beat) > (length of [beat_times])> then
            stop [this script]
```

## Best Practices

### Performance Optimization

#### Efficient Clone Management
```scratch
// Good: Limited clone creation
if <(clone_count) < (10)> then
    create clone of (myself)
    change [clone_count] by (1)

// Bad: Unlimited clone creation
create clone of (myself) // Can cause lag
```

#### Smooth Animation Parameters
```scratch
// Recommended speed values:
// Fast movement: 10-20
// Normal movement: 20-40  
// Slow/smooth: 40-80
// Very smooth: 80-120

call advanced smooth glide to x: (200) y: (100) size: (150) direction: (45) speed: (30)
```

#### Costume Effect Optimization
```scratch
// Good: Appropriate frame counts
call FX:: Costume Start: (1) End: (20) Duration (0.1)

// Consider performance: Large ranges
call FX:: Costume Start: (1) End: (312) Duration (0.05) // May cause slowdown
```

### Visual Design Guidelines

#### Layer Management
```scratch
// Background elements
go to back
go forward (2) layers

// Midground elements  
go forward (5) layers

// Foreground/UI elements
go to front
```

#### Color and Effect Coordination
```scratch
// Consistent color theming
set [color] effect to (120) // Blue theme
set [brightness] effect to (20)

// Progressive effect builds
change [ghost] effect by (-10) // Fade in
change [size] by (5) // Gentle growth
```

### Timing and Pacing

#### Natural Animation Timing
```scratch
// Fast intro elements: 0.5-2 seconds
// Main content: 3-8 seconds  
// Transition effects: 1-3 seconds
// Outro/cleanup: 2-4 seconds

wait (0.8) seconds // Quick pause
wait (2.5) seconds // Medium pause
wait (1.2) seconds // Transition time
```

## Troubleshooting Common Issues

### Animation Problems

#### Jerky Movement
**Problem**: Animations appear choppy or stuttering
**Solution**: 
- Increase speed parameter for smoother motion
- Reduce the number of simultaneous animations
- Use appropriate costume switching intervals

```scratch
// Instead of:
call advanced smooth glide to x: (200) y: (100) size: (150) direction: (45) speed: (5) // Too fast

// Use:
call advanced smooth glide to x: (200) y: (100) size: (150) direction: (45) speed: (25) // Smoother
```

#### Effects Not Appearing
**Problem**: FX costume animations don't show
**Solution**:
- Verify costume names and numbers
- Check if sprite is visible and properly sized
- Ensure costume range is valid

```scratch
// Diagnostic check
if <(costume [number]) > (costume count)> then
    switch costume to [Null] // Reset to safe costume
```

### Clone Issues

#### Too Many Clones
**Problem**: Project slows down or crashes
**Solution**:
- Implement clone cleanup
- Limit maximum clone count
- Use timer-based deletion

```scratch
// Clone cleanup pattern
when I start as a clone
// Clone behavior here
wait until <(timer) > (Time End Intro)>
delete this clone
```

#### Clone Behavior Not Working
**Problem**: Clones don't perform expected actions
**Solution**:
- Verify Clone ID is set before creating clone
- Check if/else conditions in clone initialization
- Ensure global variables are accessible

```scratch
// Proper clone creation
set [Clone ID] to [Chevron]
create clone of (myself)
set [Clone ID] to [] // Clear for next use
```

### Timing Synchronization

#### Effects Out of Sync
**Problem**: Timed effects don't align properly
**Solution**:
- Use consistent timer reference
- Account for processing delays
- Test timing with different project loads

```scratch
// Reliable timing pattern
reset timer
wait until <(timer) > (exact_time)>
// Effect happens here
```

## Advanced Examples

### Complete Intro Sequence
```scratch
when flag clicked
// Initialize
call Reset:: X: (0) Y: (0) Size: (100) Hide? (y) Direction: (90)
set [Time Start intro] to [0]
set [Time End Intro] to [20]
reset timer

// Opening impact
show
call Shake: End size (150) Intensity (25)
wait (1) seconds

// Layer buildup
set [Clone ID] to [Bars]
create clone of (myself)
wait (0.5) seconds

set [Clone ID] to [Chevron]
create clone of (myself)
wait (0.3) seconds

// Main animation sequence
call [EASING] Quintic :: Speed: (35) X: (100) Y: (-75) Size: (200) Direction: (45)
wait (3) seconds

// Effect cascade
call FX:: Costume Start: (1) End: (30) Duration (0.12)
wait (2) seconds

// Secondary movement
call advanced smooth glide to x: (-150) y: (50) size: (80) direction: (270) speed: (40)
wait (2) seconds

// Closing sequence
call Shake (.5) | (100) (15)
wait (1) seconds

call advanced smooth glide to x: (0) y: (300) size: (50) direction: (90) speed: (30)
```

### Interactive Effect Trigger
```scratch
when this sprite clicked
// User-triggered effect
call Shake: End size (120) Intensity (20)
call FX:: Costume Start: (10) End: (25) Duration (0.1)

// Reset after effect
wait (2) seconds
call Reset:: X: (0) Y: (0) Size: (100) Hide? () Direction: (90)
```

This guide provides comprehensive coverage of the Intro Engine v0.2 capabilities and practical implementation strategies.