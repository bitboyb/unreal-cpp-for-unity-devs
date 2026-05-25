# Blueprints and C++

Most Unreal teams use both.

## When to Use Each

| Task | Prefer C++ | Prefer Blueprint | Notes |
|---|---|---|---|
| Core gameplay systems | Yes | Sometimes | C++ is usually better for reusable foundations. |
| Rapid iteration on interactions | Sometimes | Yes | Blueprints are often faster for tuning and event wiring. |
| Performance-critical loops | Yes | Sometimes | Measure first, but C++ often gives more control. |
| Designer-authored logic | Sometimes | Yes | Blueprint is more accessible to non-programmers. |
| Asset defaults and assembly | Sometimes | Yes | Blueprint classes are often the main editable asset. |
| Engine integration and custom modules | Yes | Rarely | C++ is the normal path. |

## Exposing Variables to Blueprints

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Movement")
float MoveSpeed = 600.0f;
```

## Blueprint Callable Functions

```cpp
UFUNCTION(BlueprintCallable, Category = "Combat")
void FireWeapon();
```

## Blueprint Events

### `BlueprintImplementableEvent`

Blueprint provides the implementation.

```cpp
UFUNCTION(BlueprintImplementableEvent, Category = "UI")
void ShowDamageFlash();
```

### `BlueprintNativeEvent`

C++ can provide a default implementation, and Blueprint can override it.

```cpp
UFUNCTION(BlueprintNativeEvent, Category = "Interaction")
void Interact();
```

## Blueprint Classes Based on C++ Classes

A common workflow is:

1. write a reusable C++ base class
2. create a Blueprint child class
3. assign meshes, animations, effects, and defaults in the Blueprint

This is often more natural in Unreal than trying to push every asset reference into C++.

## Good Hybrid Workflow

- keep low-level systems and reusable APIs in C++
- expose only the knobs designers need
- let Blueprint handle content assembly and event flow
- move hot or repeated logic to C++ if profiling shows a problem

## Common Mistake

A common trap is thinking Blueprints are only for beginners. In Unreal, they are a normal production tool for gameplay assembly, asset authoring, and editor-friendly workflows.

## Related Pages

- [Unreal Macros and Reflection](unreal-macros-and-reflection.md)
- [UI with UMG](ui-with-umg.md)
- [Assets and References](assets-and-references.md)
