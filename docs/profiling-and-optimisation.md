# Profiling and Optimisation

Optimisation in Unreal starts with measurement, not guesswork.

## Unity Profiler vs Unreal Tools

| Unity | Unreal | Notes |
|---|---|---|
| Unity Profiler | Unreal Insights | Detailed trace-based profiling. |
| Frame debugger habits | `stat` commands and GPU tools | Quick runtime checks before deeper capture. |

## Useful `stat` Commands

```text
stat fps
stat unit
stat game
stat gpu
```

These give a fast first look at where frame time is going.

## Unreal Insights

Unreal Insights is the deeper profiling tool for:

- CPU timing
- async work
- loading behavior
- game thread bottlenecks

If a performance issue is not obvious from `stat` commands, capture an Insights trace.

## Common Cost Areas

### Tick Cost

Too many ticking objects can add up quickly.

Ask:

- does this really need to tick every frame?
- can it use timers, events, or animation callbacks instead?

### Blueprint Performance

Blueprint is fine for many gameplay tasks, but large hot loops or repeated work may be better in C++.

Measure before moving code.

### Asset Loading

Unexpected hard references can create long loads and memory spikes.

See [Assets and References](assets-and-references.md).

### Draw Calls

Rendering cost depends on materials, mesh count, transparency, shadows, and scene complexity. The exact bottleneck varies by project.

### Collision Cost

Too many overlap checks, traces, or expensive collision settings can become costly.

## Practical Optimisation Checklist

- check `stat unit` before guessing whether the bottleneck is CPU or GPU
- disable unnecessary ticking
- profile Blueprint-heavy systems before rewriting them
- review hard references and large asset chains
- reduce expensive collision queries where possible
- test on target hardware, not only on a dev PC

## Common Mistake

A common trap is optimising by habit instead of by measurement. Unreal has many systems, and the real bottleneck is often somewhere unexpected.

## Related Pages

- [Physics and Collision](physics-and-collision.md)
- [Assets and References](assets-and-references.md)
- [Blueprints and C++](blueprints-and-cpp.md)
