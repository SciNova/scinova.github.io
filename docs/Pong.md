# Technical Description of the Classic Game Pong (1-Player vs Computer)  

Pong is a 2D arcade-style game where a player controls a horizontal paddle at the bottom of the screen to hit a ball upward, competing against a computer-controlled paddle at the top. The ball bounces vertically between paddles and horizontally off side walls. The game emphasizes responsive controls, adaptive computer behavior, and dynamic ball physics.  

---

## 1. Game Components  
### **Player Paddle**  
- Moves horizontally at a constant speed.  
- Confined within screen boundaries.  
- Fixed dimensions throughout the game.  

### **Computer Paddle**  
- Automatically tracks the ball’s horizontal position with adjustable reaction time.  
- Movement includes a randomized error margin to simulate imperfection.  
- Speed scales with difficulty progression.  

### **Ball**  
- Launches with randomized direction after scoring.  
- Speed increases incrementally at predefined intervals.  
- Rebounds off paddles and side walls, with trajectory adjustments based on impact position.  

---

## 2. Game State  
### **Score System**  
- Scores displayed numerically: player (bottom-left) and computer (top-right).  
- A point is awarded when the ball exits the opponent’s vertical boundary.  
- Match concludes when a predefined score threshold is reached.  

---

## 3. Collision Mechanics  
- Ball trajectory adjusts based on the **relative horizontal impact position** on paddles:  
  - Center hits produce minimal vertical angle deviation.  
  - Edge hits create sharper vertical angles.  
- Horizontal velocity inverts on side wall collisions.  
- Ball speed escalates after consecutive hits.  

---

## 4. Progression and Difficulty  
- Computer difficulty intensifies via:  
  - Reduced reaction delay as the player’s score increases.  
  - Gradual speed acceleration (capped at a maximum multiplier).  
  - Decreasing error margin for precision.  
- Ball reset delay shortens after scoring.  
- Victory triggers a restart with heightened difficulty.  

---

## 5. Rendering  
- **Visual Style**: Minimalist design with a vertical dashed centerline.  
- **Performance**: Targets consistent frame rate and sub-10ms input latency.  
- **UI Elements**:  
  - Player Score: Bottom-left numerical display (7-segment style).  
  - Computer Score: Top-right numerical display.  
  - Victory/Defeat Banner: Centered text overlay.  

---

## 6. Config Parameters  
**All values scale with screen dimensions and use real-time calculations**  

| **Category**          | **Parameter**                     | **Value**                                  |  
|-----------------------|-----------------------------------|--------------------------------------------|  
| **Player Paddle**     | Width                             | 20% of screen width                       |  
|                       | Height                            | 2% of screen height                       |  
|                       | Movement Speed                    | 200% screen width/sec                     |  
| **Computer Paddle**   | Base Reaction Delay               | 0.25 sec                                  |  
|                       | Minimum Reaction Delay            | 0.05 sec                                  |  
|                       | Error Margin                      | ±8% of paddle width                       |  
|                       | Movement Speed                    | 180% screen width/sec                     |  
| **Ball**              | Initial Speed                     | 150% screen height/sec                    |  
|                       | Max Speed                         | 400% screen height/sec                    |  
|                       | Speed Increase Interval           | Every 10 hits                             |  
|                       | Speed Increment                   | +8% per interval                          |  
|                       | Serve Angle Range                 | ±15° (vertical)                           |  
| **Game State**        | Win Condition                     | 11 points                                 |  
|                       | Ball Reset Delay                  | 1 sec                                     |  
|                       | Difficulty Step per Player Point  | -0.015 sec reaction delay                 |  
|                       | Power-Up Spawn Chance             | 12%                                       |  
| **Input**             | Move Left                         | Left Arrow                                |  
|                       | Move Right                        | Right Arrow                               |  
| **Colors**            | Paddles/Ball                      | #FFFFFF                                   |  
|                       | Background                        | #000000                                   |  
|                       | Centerline                        | #FFFFFF (dashed, 40% opacity)             |  

---

## IMPLEMENTATION  

A complete working and playable game with all the details as per the specs, as a one-file HTML/JavaScript/CSS with metadata viewport for mobiles.