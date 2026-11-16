# Pool shot simulator

Which directions can you hit the cue ball so it reaches the red ball in one strike?

- Cue ball at (0, 0), radius 1
- Red ball at (0, 5), radius 1
- Rails at x = 5, x = -5, and y = 10 (the bottom is open)
- A shot counts when the cue ball touches the red ball, after any number of rail bounces

## Files

Just one: `index.html`. It has no build step and no dependencies. The only external request is Google Fonts, and the page falls back to system fonts if that fails.

## Publish on GitHub Pages

1. Create a new repository on GitHub (for example `pool-shot-simulator`). Public is simplest.
2. Add `index.html` and this `README.md` to the repository root (use "Add file > Upload files" on the repo page).
3. Go to Settings > Pages. Under "Build and deployment", set Source to "Deploy from a branch", choose the `main` branch and the `/ (root)` folder, then save.
4. After a minute or two, your page is live at `https://YOUR-USERNAME.github.io/pool-shot-simulator/`.

To use it on Substack, paste that URL into a post. Substack shows it as a link card.

## Change the setup

The constants are at the top of the `<script>` block in `index.html`:

```js
var CUE={x:0,y:0,r:1}, RED={x:0,y:5,r:1}, RAIL_X=5, RAIL_Y=10, MAXB=400;
```

Edit the ball positions, the radii, or the rail positions and reload. The hit-range table in the page's "The math" section is written out by hand for the default setup, so update it if you change the constants.

## How it works

The simulator follows the cue ball's center. The balls touch when their centers are `CUE.r + RED.r` apart, and the ball bounces when its edge reaches a rail, which means its center bounces off rails moved inward by `CUE.r`. A shot at angle θ hits the red ball when the center path passes within `CUE.r + RED.r` of the red ball's center. Without bounces, that condition is `|a sin θ - b cos θ| <= r`, where (a, b) is the red ball's center and r is the sum of the radii.
