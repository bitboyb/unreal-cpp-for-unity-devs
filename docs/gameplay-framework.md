# Gameplay Framework

Unreal's gameplay framework is one of the biggest differences from Unity.

## Main Classes

| Class | Role | Network Notes |
|---|---|---|
| `GameMode` / `GameModeBase` | Match rules, spawning, class defaults | Server only in networked games. |
| `GameState` / `GameStateBase` | Shared match state | Replicated to clients. |
| `PlayerController` | Player control and input ownership | Exists on server and owning client. |
| `PlayerState` | Replicated player data | Shared with clients. |
| `Pawn` | Possessable actor | Usually replicated if part of gameplay. |
| `Character` | Pawn with movement system | Common player and AI avatar type. |
| `HUD` | Legacy HUD bootstrap or debug drawing | Usually local UI-related role. |
| `GameInstance` | App-wide persistent object | Persists across level loads. |
| `World` | Runtime world context | Owns actors and level state. |
| `Level` | Map content | One world can contain one persistent level and streamed sublevels. |

## `GameMode`

### Unity Version

The rough comparison is a server-authoritative game rules manager.

### Unreal Version

`GameMode` decides:

- default pawn class
- player controller class
- spawn rules
- win and loss rules

### Key Difference

Clients do not have authoritative access to `GameMode` in a networked match because it exists only on the server.

## `GameState`

Put shared match data here when clients need to read it.

Examples:

- remaining match time
- team scores
- round state

## `PlayerController`

Use `PlayerController` for player intent and ownership-focused logic.

Examples:

- mapping contexts
- menu input mode
- cursor handling
- possession changes

## `PlayerState`

Use `PlayerState` for replicated player data that should outlive a single pawn.

## `Pawn` and `Character`

The pawn is what gets possessed. The controller is who gives the orders.

That separation is one of the most important Unreal design patterns to understand.

## `GameInstance`

`GameInstance` persists across level transitions.

Use it for:

- global services
- session data
- startup systems

Do not use it as a dumping ground for every gameplay reference.

## `World` and `Level`

`UWorld` is the runtime world context. A level is map content loaded into a world.

This matters when you work with:

- actor spawning
- traces
- timers
- streaming

## Common Mistake

A common trap is putting replicated, client-visible match data in `GameMode`. If clients need it, it usually belongs in `GameState` or `PlayerState`.

## Related Pages

- [Actors, Pawns and Characters](actors-pawns-and-characters.md)
- [Input](input.md)
- [Networking and Replication](networking-and-replication.md)
