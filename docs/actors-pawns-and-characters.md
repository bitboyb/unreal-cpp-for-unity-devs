# Actors, Pawns and Characters

This page explains the main gameplay classes Unity developers meet early in Unreal.

## Comparison Table

| Unreal Class | Rough Unity Equivalent | Typical Use |
|---|---|---|
| `UObject` | Plain managed object / Scriptable helper object | Base type for many non-level objects. |
| `AActor` | `GameObject` with one main script role | Any object that can exist in a level or be spawned. |
| `APawn` | Controllable scene object | A controllable actor for player or AI possession. |
| `ACharacter` | Character controller based object | Pawn with built-in movement support for humanoid-style characters. |
| `APlayerController` | Input/session controller role | Handles player input and possession. |
| `AGameModeBase` | Server-side game rules manager | Defines match rules and spawning on the server. |
| `AGameStateBase` | Replicated shared match state | Holds game state clients should know about. |
| `APlayerState` | Replicated player session data | Holds player score, name, and replicated player data. |
| `AHUD` | Legacy HUD manager | Draw HUD elements or own UI bootstrap logic. |

## `UObject`

### Unreal Version

`UObject` is the base class for many engine-managed objects that are not necessarily placeable in a level.

```cpp
UCLASS(BlueprintType)
class MYGAME_API UInventoryItem : public UObject
{
    GENERATED_BODY()
};
```

### Key Difference

Not everything in Unreal is an Actor. Many systems use `UObject`-based classes for data, assets, and helper objects.

## `AActor`

### Unity Version

The rough comparison is a `GameObject` that exists in the world.

### Unreal Version

`AActor` is the base class for level-placeable and spawnable gameplay objects.

```cpp
UCLASS()
class MYGAME_API APickup : public AActor
{
    GENERATED_BODY()
};
```

### Common Mistake

Do not assume every gameplay behavior belongs on a custom Actor subclass. Sometimes a Component or Controller is a better fit.

## `APawn`

`APawn` is an Actor that can be possessed by a controller.

```cpp
UCLASS()
class MYGAME_API ADronePawn : public APawn
{
    GENERATED_BODY()
};
```

Use it when the object is controllable but does not need the full character movement stack.

## `ACharacter`

`ACharacter` is a Pawn with built-in character movement support.

```cpp
UCLASS()
class MYGAME_API AHeroCharacter : public ACharacter
{
    GENERATED_BODY()
};
```

Use it for common walking, jumping, crouching, and networked character movement cases.

## `APlayerController`

`APlayerController` represents the player's control layer.

```cpp
UCLASS()
class MYGAME_API AMyPlayerController : public APlayerController
{
    GENERATED_BODY()
};
```

It often handles:

- input mapping setup
- possession
- cursor and camera decisions
- UI ownership

## `AGameModeBase`

`AGameModeBase` defines game rules, default classes, and spawning behavior.

```cpp
UCLASS()
class MYGAME_API AMyGameMode : public AGameModeBase
{
    GENERATED_BODY()
};
```

Important difference: in a networked game, `GameMode` exists only on the server.

## `AGameStateBase`

`AGameStateBase` stores game-wide state that can be replicated to clients.

```cpp
UCLASS()
class MYGAME_API AMyGameState : public AGameStateBase
{
    GENERATED_BODY()
};
```

Put shared match information here, not in `GameMode`, if clients need to read it.

## `APlayerState`

`APlayerState` stores per-player replicated data.

```cpp
UCLASS()
class MYGAME_API AMyPlayerState : public APlayerState
{
    GENERATED_BODY()
};
```

Typical examples:

- score
- player name
- team
- match-specific status

## `AHUD`

`AHUD` is older than UMG, but it still appears in projects.

```cpp
UCLASS()
class MYGAME_API AMyHUD : public AHUD
{
    GENERATED_BODY()
};
```

In many UE5 projects, UMG widgets do most visible UI work, while HUD may bootstrap widgets or draw debug elements.

## Related Pages

- [Gameplay Framework](gameplay-framework.md)
- [Components](components.md)
- [Input](input.md)
- [Networking and Replication](networking-and-replication.md)
