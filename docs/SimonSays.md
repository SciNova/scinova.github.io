# Technical Description of the Simon Says Memory Game  

Simon Says is a memory-based game where players replicate an escalating sequence of visual and auditory cues emitted by four color pads. The game tests recall accuracy through progressively complex patterns, with synchronized sound feedback and adaptive difficulty.  

---

## 1. Game Components  
### **Color Pads**  
- A set of interactive pads arranged symmetrically (each pad resembling a quarter of a cut pie: upper left, upper right, lower right and lower left, numbered in this order from 1 to 4.
- Each pad emits a unique tone and highlights on activation.  
- Visual feedback includes brightness  and border color highlight when playing a sound.  

### **Game Controller**  
- Generates randomized sequences of increasing length.  
- Validates player input against the active sequence in real time.  
- Manages timing thresholds for input validation.
- Failing to repeat a sequence will show the same sequence again.

### **Audio/Visual Feedback**  
- Distinct frequencies assigned to each pad.  
- Error and success sounds triggered on input validation.  
- VERY visible visual feedback of the pads when they play a sound.  
- **Web Audio Best Practices**:  
  - Initialize audio on first user interaction (e.g., button press).  
  - Use dedicated audio nodes per sound event with proper routing.  
  - Terminate audio nodes after playback to prevent resource leaks.  

---

## 2. Game State  
### **Scoring System**  
- Points awarded per correctly replicated step.  
- Combo multipliers for consecutive flawless sequences.  
- Score deductions for errors or exceeded time limits.  

### **Lives & Progression**  
- Lives decremented on incorrect input or timeout.  
- Bonus lives granted at predefined score milestones.  
- Game over on life depletion, with progress saved locally.  

### **Level Advancement**  
- Sequence length increases progressively per level.  
- Speed of sequence playback scales with difficulty.  
- Victory achieved upon completing all configured levels.  

---

## 3. Input Mechanics  
- **Pad Interaction**: Touch, mouse, or keyboard input.  
- **Timing Constraints**:  
  - Max delay between sequence end and player input.  
  - Max delay between consecutive player inputs.  
- Inputs ignored during sequence playback.  

---

## 4. Progression and Difficulty  
- Difficulty escalates via:  
  - Faster sequence playback speeds.  
  - Reduced time limits for player input.  
  - Introduction of parallel sequences (optional).  
  - Randomized pauses within sequences.  
- Pad highlight duration shortens at higher levels.  
- Error tolerance decreases after predefined stages.  

---

## 5. Rendering & Performance  
- **Visual Design**:  
  - Pads retain minimal brightness when inactive.  
  - Smooth animations for pad highlights and errors.  
  - Progress bar indicating remaining input time.  
- **Audio Design**:  
  - Stereo panning based on pad position.  
  - Dynamic volume scaling with sequence speed.  
- **Performance**:  
  - Audio playback with near-zero latency.  
  - Frame rate synchronized to screen refresh rate.  

---

## 6. Config Parameters  

| **Category**          | **Parameter**                     | **Value**                                  |  
|-----------------------|-----------------------------------|--------------------------------------------|  
| **Game Setup**        | Number of Pads                   | 4                                         |  
|                       | Pad Colors                       | #FF0000, #00FF00, #0000FF, #FFFF00        |  
|                       | Initial Sequence Length          | 3                                         |  
|                       | Sequence Increment per Level     | +1                                        |  
|                       | Max Levels                       | 20                                        |  
| **Timing**            | Sequence Playback Speed          | 800 ms per step (initial)                 |  
|                       | Playback Speed Decrement per Level | -25 ms                                   |  
|                       | Max Input Delay After Sequence   | 3000 ms                                   |  
|                       | Max Input Delay Between Steps    | 1500 ms                                   |   
| **Audio**             | Pad Tone Frequencies             | 440 Hz, 554 Hz, 659 Hz, 880 Hz            |  
|                       | Error Sound Frequency            | 220 Hz                                    |  
|                       | Tone Duration                    | 300 ms                                    |  
| **Scoring**           | Points per Correct Step          | 100                                       |  
|                       | Combo Multiplier Increment       | ×1.2 per 5 consecutive correct sequences  |  
|                       | Error Penalty                    | -200 points                               |  
| **Lives**             | Initial Lives                    | 3                                         |  
|                       | Bonus Life Threshold             | Every 5000 points                         |  
| **Visual**            | Highlight Animation Duration     | 200 ms                                    |  
|                       | Error Flash Duration             | 500 ms                                    |  
| **Input**             | Touch/Mouse Input                | Enabled                    |  

---

## IMPLEMENTATION  

A complete working game with all specified features, including sound and visual feedback, as a single HTML/JavaScript/CSS file. Includes mobile viewport optimization and localStorage for progress tracking.