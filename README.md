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

## Credits

The algorithm and the palette come from Fabien Sanglard's article [How DOOM fire was done](https://fabiensanglard.net/doom_fire_psx/).
