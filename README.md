# doom_fire

The fire effect from the PlayStation version of Doom, in the terminal. Written in Rust.

## Run

```
cargo run --release
```

Use a terminal that supports 24-bit color, such as iTerm2, Ghostty, kitty or WezTerm.

Press Ctrl-C to stop. The program hides the cursor. To show it again, run `tput cnorm`.

## How it works

- The fire is a grid of heat values, from 0 (cold) to 36 (hot).
- The bottom row is always 36. It is the source of the fire.
- On each frame, each pixel gets the heat of the pixel below it, minus a small random value. The same random value also moves the heat a little to the left.
- A palette of 37 colors changes each heat value into a color: black, red, orange, yellow, then white.

## Formula

The pixel at column `x` and row `y` has the index `i = y * WIDTH + x`. Row 0 is the top.

On each frame, for each pixel that is not in the bottom row:

```
decay           = random integer: 0, 1 or 2
fire[i - decay] = max(fire[i + WIDTH] - decay, 0)
```

- `fire[i + WIDTH]` is the pixel directly below.
- `- decay` on the heat makes the fire cooler as it rises.
- `- decay` on the index moves the heat 0, 1 or 2 pixels to the left, like wind.

The color of heat value `v` is `(PALETTE[3v], PALETTE[3v + 1], PALETTE[3v + 2])`.

## Credits

The algorithm and the palette come from Fabien Sanglard's article [How DOOM fire was done](https://fabiensanglard.net/doom_fire_psx/).
