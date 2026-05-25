# Physics and Collision

Unity and Unreal both support real-time physics, but the setup model is different.

## Rigidbody vs Unreal Physics Components

### Unity Version

In Unity, physics usually centres around `Rigidbody` and collider components.

### Unreal Version

In Unreal, physics usually lives on `UPrimitiveComponent` subclasses such as `UStaticMeshComponent` or `UCapsuleComponent`.

### Key Difference

The Actor is not the physics body by itself. Its primitive components usually carry the collision and simulation settings.

## Collision Concepts

| Unity | Unreal | Notes |
|---|---|---|
| Layers | Collision channels | Used to filter interactions. |
| Layer collision matrix | Object responses | Per-channel block, overlap, or ignore response. |
| Trigger collider | Overlap event | Usually uses overlap responses rather than blocking. |
| Raycast | Trace / line trace | Common for weapons, interaction, and visibility tests. |

## Applying Forces and Impulses

#### Unity C#

```csharp
var rb = GetComponent<Rigidbody>();
rb.AddForce(Vector3.up * 10f, ForceMode.Impulse);
```

#### Unreal C++

```cpp
if (UPrimitiveComponent* Primitive = FindComponentByClass<UPrimitiveComponent>())
{
    Primitive->AddImpulse(FVector(0.0f, 0.0f, 1000.0f));
}
```

## Overlap Events

```cpp
TriggerCapsule->OnComponentBeginOverlap.AddDynamic(this, &AMyActor::HandleOverlapBegin);
```

Use overlap events when you want detection without a blocking collision response.

## Hit Events

```cpp
MeshComponent->OnComponentHit.AddDynamic(this, &AMyActor::HandleHit);
```

Hit events are usually for blocking collisions.

## Traces

#### Unity C#

```csharp
if (Physics.Raycast(transform.position, transform.forward, out RaycastHit hit, 500f))
{
    Debug.Log(hit.collider.name);
}
```

#### Unreal C++

```cpp
FHitResult Hit;
FVector Start = GetActorLocation();
FVector End = Start + GetActorForwardVector() * 500.0f;

GetWorld()->LineTraceSingleByChannel(Hit, Start, End, ECC_Visibility);
```

## Collision Channels and Responses

Unreal lets you define what each object type does when meeting another channel:

- `Block`
- `Overlap`
- `Ignore`

This is more explicit than many beginner Unity setups and is worth learning early.

## Common Mistake

A common trap is checking Actor tags and ignoring collision configuration. In Unreal, many collision bugs are really channel and response setup problems.

## Related Pages

- [Components](components.md)
- [Profiling and Optimisation](profiling-and-optimisation.md)
- [Glossary](glossary.md)
