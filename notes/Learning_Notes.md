# AI Learning & Development Notes

## What I Learned
Throughout this assessment, I focused on learning how to effectively guide AI to produce specific, usable outputs rather than generic responses. 
* **Prompt Engineering:** I learned that basic instructions (e.g., "give me a game idea") result in ideas that are too broad. By studying the `agentskills.io` structure, I learned how to constrain the AI using formatting requirements (Title, Core Mechanic, UI Elements). This forced the AI to generate a hyper-casual, single-tap game concept that perfectly fit the scope of a lightweight browser game.
* **Cross-Platform Controls:** I learned how to use AI to seamlessly implement both `mousedown` (desktop) and `touchstart` (mobile) event listeners on the global window, ensuring the game is fully playable on any device without double-firing events.

## Problems Identified & Solved

While playtesting the generated game, I identified and fixed two major issues:

**1. The Event Propagation Bug (Controls)**
* **Problem:** When I clicked the "Start Game" button, the game instantly registered that click as my first gameplay move. Because the dial wasn't in the green zone yet, the game immediately ended with a "Missed" state.
* **Fix:** I updated the JavaScript by passing the event object `(e)` into the button's click listener and adding `e.stopPropagation()`. This verified fix prevented the initial click from bubbling up to the global window listeners.

**2. Lack of Urgency (Game Loop)**
* **Problem:** The original code allowed the player to wait indefinitely for the dial to align perfectly, making the game too easy and lacking a clear failure condition aside from a bad click.
* **Fix:** I used AI to help integrate a `deltaTime` countdown timer into the `requestAnimationFrame` game loop. I gave the player exactly 5.0 seconds per level. If `timeLeft <= 0`, it now correctly triggers the `endGame(false)` function and displays a "Time Out" message.
