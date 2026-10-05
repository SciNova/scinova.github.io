# Technical Description of the Classic Game Breakout  

Breakout is a 2D arcade-style game where players use a paddle to deflect a ball upward, destroying an arrangement of bricks. The game features precise collision detection, dynamic ball physics, and progressive difficulty scaling.  

---

## 1. Game Components  
### **Paddle**  
- Moves horizontally at a constant speed.  
- Width decreases progressively with each level, starting from an initial size.  
- Confined within screen boundaries.  
- Resets to its initial width at the start of each level.  

### **Ball**  
- Launches with predefined velocities that scale with the screen dimensions.  
- Speed changes are applied as percentages of its current velocity.  
- Rebounds off walls, the paddle, and bricks.  

### **Bricks**  
- Arranged in a uniform grid centered horizontally, positioned a fixed distance from the top of the screen.  
- Percentage-based effects (e.g., paddle width changes) are calculated relative to initial values.  
- Multi-hit bricks display damage states corresponding to remaining durability.  

---

## 2. Game State  
### **Score System**  
- Updates dynamically with brick destruction.  
- Deductions visually highlight in red.  
- Base brick value scales with row height.  
- Multi-hit bricks award partial points per collision.  
- Consecutive hits within a time window trigger combo multipliers.  

### **Life Management**  
- Lives lost immediately if the ball exits the play area.  
- Bonus lives granted at predefined score thresholds.  

### **Power-Ups & Penalties**  
- Active effects display as status icons with duration indicators.
- Effects do not persist between levels 
- Timed effects pulse during activation and expire visibly.  

### **Level Progression**  
- Requires destruction of all breakable bricks.  
- Transition sequence pauses gameplay, clears debris, and resets core elements.  

---

## 3. Collision Mechanics  
- Ball trajectory adjusts based on the **relative position of impact** on the paddle.  
- Percentage-based velocity changes apply to the ball’s current speed.  
- Teleport bricks randomize the ball’s position within the play area and alter its trajectory within a fixed angular range.  


---

## 4. Progression and Difficulty  
- Difficulty increases via:  
  - Hazard brick introduction.  
  - Progressive ball acceleration.  
  - Gradual paddle width reduction.  
  - Reduced availability of destructible bricks.  
- Special bricks appear more frequently in later levels.  
- Bonus lives reward high-score milestones.  
- The game concludes upon completing all available levels.  

---

## 5. Rendering  
- **Visual Style**: Minimalist design with distinct markers for special bricks.  
- **Performance**: Maintains steady frame rate and instantaneous input responsiveness.  
- **UI Elements**:  
  - Score: Top-left numerical display (7-segment style).  
  - Level Number: Segmented digits below the score.  
  - Lives Indicator: Centered paddle icons.  
  - Status Effects: Icons with circular progress rings for duration.  

---

## 6. Config Parameters  
**All values scale with screen dimensions and use real-time calculations**  

| **Category**          | **Parameter**                     | **Value**                                  |  
|-----------------------|-----------------------------------|--------------------------------------------|  
| **Screen**            | Base Resolution                   | 800×600 (scales to device, keeping the aspect ratio)                |  
| **Paddle**            | Initial Width                     | 10% of screen width                       |  
|                       | Width Decrease per Level          | 1% of screen width                        |  
|                       | Minimum Width                     | 10% of screen width                       |  
|                       | Height                            | 2% of screen height                       |  
|                       | Movement Speed                    | 45% screen width/sec                      |  
| **Ball**              | Initial Vertical Velocity         | -120% screen height/sec (upward)          |  
|                       | Initial Horizontal Velocity       | Randomized ±120% screen width/sec         |  
|                       | Speed Increase (per 4 hits)       | +5% velocity (capped at 240% screen height/sec) |  
| **Bricks**            | Grid Size                         | 8 rows × 10 columns                       |  
|                       | Brick Dimensions                  | 5% width × 3.33% height                   |  
|                       | Spacing                           | 0.25% screen width                        |  
|                       | Points per Row (Row 1–8)          | 10, 20, 30, ..., 80                       |  
|                       | **Hazard: Paddle Width Reduction**| -10% width for 5 sec                      |  
|                       | **Hazard: Ball Speed Increase**   | +10% permanent velocity                   |  
|                       | **Hazard: Points Deduction**      | -50 points                                |  
|                       | **Bonus: Extra Life**             | +1 life                                   |  
|                       | **Bonus: Ball Slowdown**          | -30% velocity for 5 sec                   |  
|                       | **Bonus: Paddle Boost**           | +20% width for 8 sec                      |  
|                       | **Multi-Hit Requirement**         | 3 collisions                              |  
|                       | **Teleport Angle Variance**       | ±20°                                      |  
|                       | **Non-Destructive Spawn Rate**    | 10% of grid (max 4/level)                 |  
| **Game State**        | Initial Lives                     | 3                                         |  
|                       | Total Levels                      | 10                                        |  
|                       | Bonus Life Threshold              | 10,000 points                             |  
|                       | Combo Window                      | 2 sec                                     |  
|                       | Level Transition Delay            | 2 sec                                     |  
|                       | Ball Reset Delay                  | 1.5 sec                                   |  
| **Input**             | Move Left                         | Left Arrow                                |  
|                       | Move Right                        | Right Arrow                               |  
|                       | Launch Ball                       | Spacebar                                  |  
| **Colors**            | Paddle/Ball                       | #FFFFFF                                   |  
|                       | Brick Gradient                    | #FF0000 (Row 1) → #FFFF00 (Row 8)         |  

---

## IMPLEMENTATION

A complete working and playable game with all the details as per the specs, as a one-file html/javascript/css with metadata viewport for mobiles.
