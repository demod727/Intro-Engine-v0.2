# Function Reference - Intro Engine v0.2

## Core Functions

### Animation Functions

#### `[EASING] Quintic`
```scratch
define [EASING] Quintic :: Speed: (speed) X: (x position) Y: (y position) Size: (size) Direction: (direction)
```

**Implementation Details**:
- Initializes EASING list with current sprite state: `[current x, current y, current size, current direction]`
- Executes smooth quintic interpolation over `speed` iterations
- Uses mathematical formulas for smooth acceleration/deceleration curves
- Supports both acceleration and deceleration phases based on progress

**Mathematical Foundation**:
- For t < 0.5: Uses `16 * t^5` formula for acceleration
- For t >= 0.5: Uses `1 + 16 * (t-1)^5` formula for deceleration
- Progress calculated as `count * 2` where count increments by `1/speed`

**Side Effects**:
- Modifies sprite position, size, and direction
- Updates EASING list during execution
- Changes `count` variable for progress tracking

---

#### `advanced smooth glide to`
```scratch
define advanced smooth glide to x: (x) y: (y) size: (size) direction: (direction) speed: (speed)
```

**Implementation Details**:
- Continues until all parameters match targets (rounded to nearest integer)
- Incremental changes: `(target - current) / speed`
- Handles four properties simultaneously with independent convergence
- Uses repeat until loop with compound condition checking

**Convergence Logic**:
```scratch
repeat until <(round(x position) = round(x)) and (round(y position) = round(y)) and (round(size) = round(size)) and (round(direction) = round(direction))>
```

**Performance**: 
- Speed parameter directly affects smoothness vs. performance
- Lower speed values = faster movement, higher = smoother

---

### Visual Effects Functions

#### `Shake: End size`
```scratch
define Shake: End size (End size) Intensity (Intensity)
```

**Implementation Details**:
1. **Initialization**: Sets size to 120, prepares shake parameters
2. **Shake Loop**: Repeats `Intensity` times
   - X movement: `sin(End size) / 7` 
   - Y movement: `sin(End size) / 7`
   - Size change: `(round(End size) - current size) / 7`
   - Updates Camera Control list indices 2 and 3
3. **Reset**: Returns to (0,0) position, updates camera control

**Camera Integration**:
- Modifies global Camera Control list for screen-wide effects
- Index 2: X camera offset
- Index 3: Y camera offset

**Mathematical Pattern**:
- Uses sine function of End size parameter for organic movement
- Division by 7 provides appropriate scaling
- Rounded End size ensures integer calculations

---

#### `Shake (.5)`
```scratch
define Shake (.5) | (End-Size) (Repeat)
```

**Alternative Implementation**:
- Timer-based instead of iteration-based
- Uses `sin(timer * 1000)` and `sin(timer * 800)` for X/Y
- Multiplier of 0.5 for gentler movement: `(size - End-Size) * 0.5`
- Real-time camera control updates
- Size transitions: `(End-Size - current size) / 7`

**Timing Characteristics**:
- X movement frequency: 1000 rad/sec
- Y movement frequency: 800 rad/sec  
- Creates slightly elliptical movement pattern

---

#### `FX:: Costume Start: End:`
```scratch
define FX:: Costume Start: (Start Cos. #) End: (End Cos. #) Duration (Dur.)
```

**Implementation Details**:
1. **Initialization**: Switch to starting costume number
2. **Special Case**: If Start Cos. # = 312, use instant transitions (0.1s delay)
3. **Normal Case**: Use specified duration between frames
4. **Progression**: `next costume` until reaching End Cos. #

**Costume Numbering**:
- Costumes numbered sequentially starting from 1
- Special handling for costume 312 (likely end of major sequence)
- Supports both forward and backward animation by parameter order

**Usage Patterns**:
- Forward: `Start: (1) End: (20)` 
- Reverse: `Start: (20) End: (1)`
- Loop: Call repeatedly with same parameters

---

### Sprite Management Functions

#### `Reset::`
```scratch
define Reset:: X: (X) Y: (Y) Size: (Size) Hide? (Hide?) Direction: (Dir)
```

**Implementation Details**:
1. **Positioning**: `go to x: (X) y: (Y)`
2. **Sizing**: `set size to (Size)%`
3. **Visibility**: Hide if Hide? = "y", otherwise show
4. **Rotation**: `point in direction (Dir)`
5. **Effects**: Clear all graphic effects

**Parameter Validation**:
- X, Y: Any numeric values (including negative)
- Size: Percentage value (100 = normal size)
- Hide?: String comparison (case-sensitive "y")
- Direction: 0-360 degrees (0 = up, 90 = right)

**Common Usage**:
```scratch
call Reset:: X: (0) Y: (0) Size: (100) Hide? () Direction: (90)
```

---

## Block-Level Functions

### Clone Management

#### Clone Initialization Blocks
Each clone type has specialized initialization:

##### Chevron Clone (`Clone ID = "Chevron"`)
```scratch
when I start as a clone
if <(Clone ID) = [Chevron]> then
    switch costume to [Size Hack]
    call Reset:: X: () Y: () Size: () Hide? (y) Direction: (90)
    show
    set [____(For this sprite only) Chev size] to [0]
    repeat (75)
        // Chevron-specific animation
        go to back (5) layers
        switch costume to [Size Hack]
        change size by ((Chev size - size) / 3)
        change [____(For this sprite only) Chev size] by (2 + (Chev size * 0.04))
        switch costume to [Chevron]
```

**Chevron Animation Logic**:
- Uses "Size Hack" costume for size calculations
- Implements smooth size growth with exponential curve
- Layer management for visual depth
- Custom variable tracking for smooth transitions

##### Chevron2 Clone (`Clone ID = "Chevron2"`)
- Similar to Chevron but with different costume switching
- Uses [Chevron2] costume instead of [Chevron]
- Same mathematical progression and timing

##### Bars Clone (`Clone ID = "Bars"`)
```scratch
when I start as a clone
if <(Clone ID) = [Bars]> then
    switch costume to [Bars]
    go to front
    call Reset:: X: () Y: () Size: (100) Hide? (y) Direction: (90)
    switch costume to [Size]
    set size to (150)%
    switch costume to [Bars]
    show
    // Size reduction animation
    repeat (100)
        change size by ((90 - size) / 7)
        go to front
    // Timer-based duration
    repeat until <(Time End Intro) < (timer)>
        go to front
    delete this clone
```

**Bars Animation Characteristics**:
- Front layer positioning for overlay effects
- Size reduction from 150% to 90%
- Timer-based duration control
- Automatic cleanup after timer expiration

---

## Utility Functions

### Mathematical Helpers

#### Easing Calculations
The engine implements several mathematical patterns:

**Quintic Easing Formula**:
```
For progress t (0 to 1):
- Acceleration phase (t < 0.5): 16 * t^5
- Deceleration phase (t >= 0.5): 1 + 16 * (t-1)^5
```

**Smooth Interpolation**:
```
change_per_frame = (target - current) / speed
```

**Sinusoidal Movement**:
```
x_offset = sin(parameter) * intensity * multiplier
y_offset = cos(parameter) * intensity * multiplier
```

#### List Management Patterns

**EASING List Structure**:
- Index 1: Starting X position
- Index 2: Starting Y position  
- Index 3: Starting size
- Index 4: Starting direction

**Camera Control List**:
- Index 1: Camera X offset
- Index 2: Camera Y offset
- Index 3: Camera scale/rotation

**FX Data List**:
- Index 1: Effect state
- Index 2: Effect mode
- Index 3-5: Effect parameters

---

## Event Handlers

### Stage Events
```scratch
when flag clicked
// Global initialization
set [variable] to [default_value]
```

### Sprite Events  
```scratch
when I start as a clone
// Clone-specific initialization based on Clone ID
```

### Timer Events
```scratch
when timer > (value)
// Time-based triggers for synchronized effects
```

---

## Performance Optimization Functions

### Efficient Looping Patterns

#### Optimized Repeat Loops
```scratch
repeat (calculated_iterations)
    // Batch operations
    // Minimize costume switches
    // Update multiple properties simultaneously
```

#### Conditional Processing
```scratch
if <condition> then
    // Expensive operations only when needed
else
    // Fallback or skip
```

### Memory Management

#### Clone Cleanup
```scratch
// Automatic cleanup in Bars clones
repeat until <(Time End Intro) < (timer)>
    // Active behavior
delete this clone
```

#### Asset Management
- Costume switching patterns minimize memory usage
- Strategic use of "Size Hack" costume for calculations
- Efficient list operations for data storage

---

## Error Handling Patterns

### Defensive Programming
```scratch
// Parameter validation
if <(parameter) = []> then
    set [parameter] to [default_value]
```

### Graceful Degradation
```scratch
// Costume fallbacks
if <costume exists> then
    switch costume to [target]
else
    switch costume to [default]
```

### State Recovery
```scratch
// Reset to known good state
call Reset:: X: (0) Y: (0) Size: (100) Hide? () Direction: (90)
```

This reference provides the technical foundation for understanding and extending the Intro Engine v0.2 functionality.