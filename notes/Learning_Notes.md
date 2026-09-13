# AI Learning & Development Notes

## What I Learned
Throughout this assessment, I focused on learning how to effectively guide AI to produce specific, usable outputs rather than generic responses. 
* **Prompt Engineering:** I learned that basic instructions (e.g., "give me a game idea") result in ideas that are too broad. By studying the `agentskills.io` structure, I learned how to constrain the AI using formatting requirements. This forced the AI to generate a hyper-casual, single-tap game concept that perfectly fit the scope of a lightweight browser game.
* **Browser APIs Without External Assets:** I learned how to use AI to generate synthesized audio using the browser's native `window.AudioContext` API. This allowed me to add sound effects directly in JavaScript without relying on external .mp3 files, keeping the project strictly single-file.

## Problems Identified & Solved

While playtesting the generated game, I identified and fixed several UX and gameplay issues to make it feel like a polished product:

**1. The Event Propagation Bug (Controls)**
* **Problem:** When I clicked the "Start Game" button, the game instantly registered that click as my first gameplay move, resulting in an instant "Miss/Game Over".
* **Fix:** I updated the JavaScript by passing the event object `(e)` into the button's click listener and adding `e.stopPropagation()`. This prevented the initial click from bubbling up to the global canvas listeners.

**2. Lack of Gameplay Urgency & Repetition**
* **Problem:** The original code had a flat 3-level structure where the player could wait indefinitely for the dial to align perfectly. 
* **Fix:** I transitioned the game to an Endless Survival Mode and added a strict `deltaTime` countdown timer. I also added a direction reversal mechanic `dialDirection *= -1;` upon every successful hit. This forces the player to recalibrate their timing constantly and prevents the game from feeling static.

**3. Missing Sensory Feedback**
* **Problem:** The game relied solely on static text changing to tell the player if they won or lost, which lacked impact.
* **Fix:** I integrated a `flashBackground()` function that briefly flashes the screen green on a hit and red on a miss. I paired this with JavaScript-generated oscillator sounds (a high-pitched sine beep for hits and a low sawtooth buzz for failures) to give immediate, satisfying feedback.
