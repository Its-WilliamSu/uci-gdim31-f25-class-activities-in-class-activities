# in-class-activities
## Devlogs

### W1

**1. In the Hierarchy, move the Camera off of the Cat GameObject, so that it's no longer a child of the Cat. What happens when you run the game now, and why?**

When the Camera is a child of the Cat, it follows the cat around because a child's Transform is relative to its parent — wherever the cat moves, the camera moves with it. After dragging the Camera out of the Cat so it becomes its own root object, the camera stays fixed in the world at whatever position it was left in. When you run the game and walk forward, the cat just walks away and leaves the camera behind, so the cat quickly walks off-screen and you end up staring at an empty platform. This happens because Transform values (position, rotation, scale) of a child are inherited from and updated with its parent; once the parenting link is broken, the cat's movement no longer affects the camera at all.

**2. Please link your working Itch page.**

[Play the W1 in-class activity on Itch.io](https://its-williamsu.itch.io/gdim31-w1-activity)

### W2

**1. Why are the r, g, and b variables floats instead of ints, bools, or strings?**

Because color channels are fractional values between 0.0 and 1.0. Each bounce only changes the color by a small amount like 0.1, so we need decimals — an int could only hold whole numbers (0 or 1, nothing in between), a bool can only be true/false, and a string is text, not a number you can do math with. Floats are the type built for storing numbers with decimals, which is exactly what colors need.

**2. Why is the _bounce variable an int instead of a float, bool, or string?**

Because _bounce counts how many times the ball has bounced, and you can only bounce a whole number of times — 0, 1, 2, 3... There's no such thing as "2.4 bounces," so a float would pretend there's more precision than actually exists. An int is the type for counting discrete whole things. (A bool could only tell us "bounced or not," and a string can't be added to with `++`.)

**3. The error you got after Step 4 of Part 2 told you something useful about why that line of code was broken — what was it?**

The line `g -= 0.1f` was missing its semicolon, and the compiler error ("; expected") told me the statement wasn't finished. That was useful because the error pointed at the exact spot where the parser got stuck — the end of that line — so I knew immediately that the previous statement was incomplete rather than having to hunt through unrelated code.

### W3

**Table number:** Not recorded; I chose a seat freely.

**Activity 1 — method designs:**

1. `GetResponse` (visual novel): parameters are an **int** (the player's current friendship level with the character) and a **bool** (whether the player knows the character's secret); return type is a **string**, because the method's whole job is to hand back the character's text response.
2. `SetLightDimness` (horror game): parameter is a **float** (the player's sanity level, 0–100); return type is **void**, because the method changes the light itself and doesn't need to hand any value back to the code that called it.
3. `DidPlayerHitBeat` (rhythm game): parameter is a **float** (the time the key was pressed, so it can be compared against the beat time); return type is a **bool** — the method only needs to answer "yes, they hit it" or "no, they missed."

**Activity 2 — classes & Components metaphor:**

A class is like a cookie cutter, and a Component is an actual cookie cut out from it and placed on the scene's baking sheet (the Scene). One cookie cutter can stamp out many cookies, just like one class can become many Component instances. Member variables are the decorating details written on each individual cookie — this one has red frosting, that one has sprinkles — so every cookie from the same cutter can still look different. Methods are the things each cookie can do: `GetEaten()`, `DunkInMilk()`. The Scene is the whole baking sheet that holds all the cookies together.

**Activity 3 — why do the balls get extremely bright if they bounce too many times?**

Because Step 9 multiplies the ball's color by 1.5 on every bounce where the ball is moving faster than the speed threshold, and multiplication like that compounds: 1.0 → 1.5 → 2.25 → 3.4 and so on, with no cap. The color channels quickly grow far past the normal 0.0–1.0 range, and Unity renders color values above 1.0 as extremely bright, oversaturated, "glowing" colors. It looks especially intense in the Scene view, where the high values blow out to near-white.

## Open-Source Assets
### W1
- Animals: https://assetstore.unity.com/packages/3d/characters/animals/animals-free-animated-low-poly-3d-models-260727 
- Low-poly environment: https://assetstore.unity.com/packages/3d/environments/landscapes/low-poly-simple-nature-pack-162153 
