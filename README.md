# Fx

Drop-in UI juice for Roblox. Particles, ripples, flashes, shakes, animated
borders, rays and cursor parallax for any UI.

Client only. No dependencies, no assets, nothing to set up.


## Install

**Model** — download `Fx.rbxm` from [Releases](https://github.com/jmhfields3-star/fx/releases)
and drag it into `ReplicatedStorage`.


**Wally**

```toml
[dependencies]
Fx = "jmhfields3-star/fx@1.0.0"
```

## Quick start

```lua
local Fx = require(game.ReplicatedStorage.Fx)

button.Activated:Connect(function()
    Fx.Burst(Fx.CenterOf(button))   -- confetti
    Fx.Ripple(Fx.MouseAbs())        -- ring at the cursor
    Fx.Flash(panel)                 -- white-out that fades
    Fx.Shake(panel)                 -- decaying jitter
end)

Fx.NeonBorder(stroke, { Color3.new(1, 0, 0), Color3.new(0, 0, 1) })
Fx.Rays(panel, UDim2.fromScale(0.5, 0.5))
Fx.SparkleOnHover(button, button)
Fx.Bob(icon)
Fx.Parallax(panel)
Fx.Dim(true)
```

The first call makes its own full-screen `ScreenGui` in `PlayerGui`. To draw
inside your own UI instead, call `Fx.Init(myScreenGui)` once first.

## Configuring

Every default lives in `Fx.Config`. Globally:

```lua
Fx.Configure({
    Burst = { Count = 30, Life = 1.4 },
    Palette = { Color3.fromRGB(255, 0, 120) },
})
```

Or per call, same keys:

```lua
Fx.Burst(position, { Count = 60, Gravity = 0, Glyphs = { "$" } })
```

Sections: `Layer`, `Glyph`, `Palette`, `MaxParticles`, `Burst`, `Ripple`,
`Flash`, `Shake`, `Neon`, `Pulse`, `Rays`, `Sparkle`, `Bob`, `Parallax`, `Dim`.

## API

| Call | Returns |
| --- | --- |
| `Fx.Init(parent?)` | `Instance` |
| `Fx.Configure(overrides)` | |
| `Fx.Burst(position, options?)` | |
| `Fx.Ripple(position, options?)` | |
| `Fx.Flash(target, options?)` | `Frame` |
| `Fx.Shake(target, options?)` | |
| `Fx.NeonBorder(stroke, colors, options?)` | `UIGradient` |
| `Fx.PulseStroke(stroke, a, b, options?)` | `UIStroke` |
| `Fx.Rays(parent, center, options?)` | `Frame` |
| `Fx.SparkleOnHover(target, clickable, options?)` | |
| `Fx.Bob(target, options?)` | `GuiObject` |
| `Fx.Parallax(target, options?)` | `GuiObject` |
| `Fx.Dim(visible, options?)` | |
| `Fx.CenterOf(target)` / `Fx.PointIn(target)` / `Fx.MouseAbs()` | `Vector2` |
| `Fx.Stop(handle)` / `Fx.Clear()` / `Fx.Destroy()` | |

Anything continuous returns a handle — pass it to `Fx.Stop` to end it.

## Notes

- **Positions are AbsolutePosition space.** Use `Fx.CenterOf`, `Fx.PointIn` and
  `Fx.MouseAbs`. Passing `UserInputService:GetMouseLocation()` straight in is off
  by the height of the top bar.
- **`Bob`, `Shake` and `Parallax` all drive `Position`** — one per element.
- **Glyph particles use a text font.** Pick one that has the characters you pass;
  most Roblox fonts have no `✦`, `♥` or `★`.
- **Performance:** the render loop only runs while something is animating, and
  particles are capped by `Fx.Config.MaxParticles` (400). Lower it for mobile.

## License

MIT — see [LICENSE](LICENSE).
