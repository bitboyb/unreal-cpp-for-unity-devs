# Components

Components are one of the easiest bridges from Unity to Unreal, but the details matter.

## Unity Components vs Unreal Components

### Unity Version

Unity uses Components attached to `GameObject`s. The transform is built into the `GameObject`.

### Unreal Version

Unreal uses Components attached to an `Actor`. Transform data usually lives on `USceneComponent` and its subclasses.

### Key Difference

In Unreal, not every component has a transform. `UActorComponent` is the non-spatial base class.

## Main Component Types

| Unreal Type | Rough Unity Equivalent | Typical Use |
|---|---|---|
| `UActorComponent` | Non-visual script component | Reusable logic or data without transform. |
| `USceneComponent` | Transform-bearing component | Parent-child transforms and attachment. |
| `UPrimitiveComponent` | Render/physics-capable scene component | Collision, rendering, overlap, and hit events. |
| `UStaticMeshComponent` | Mesh renderer plus collider role | Display static meshes and interact physically. |
| `UCameraComponent` | Camera component | Defines a camera view. |
| `USpringArmComponent` | Camera rig helper | Handles camera follow distance and lag. |

## Creating Components in a Constructor

### Example

#### Unity C#

```csharp
public class CameraFollow : MonoBehaviour
{
    private Camera cam;

    void Awake()
    {
        cam = gameObject.AddComponent<Camera>();
    }
}
```

#### Unreal C++

```cpp
AMyPawn::AMyPawn()
{
    RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("Root"));

    SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArm"));
    SpringArm->SetupAttachment(RootComponent);

    Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("Camera"));
    Camera->SetupAttachment(SpringArm);
}
```

Use `CreateDefaultSubobject` in the constructor for default components that should exist on every instance.

## `RootComponent`

The root component is the top of the Actor's component hierarchy. Moving the Actor generally moves the root and its children.

```cpp
RootComponent = MeshComponent;
```

## `FindComponentByClass`

Use this when you need to locate a component on an Actor at runtime.

```cpp
UStaticMeshComponent* Mesh = FindComponentByClass<UStaticMeshComponent>();
```

This is similar to `GetComponent<T>()` in Unity, but if the component is guaranteed to exist, a stored member pointer is often clearer.

## Common Mistake

A common trap is creating gameplay-critical default components late in `BeginPlay` instead of in the constructor. If the component should always exist, create it as a default subobject so it is visible in defaults, Blueprints, and inherited classes.

## Related Pages

- [Actors, Pawns and Characters](actors-pawns-and-characters.md)
- [Lifecycle and Events](lifecycle-and-events.md)
- [Physics and Collision](physics-and-collision.md)
