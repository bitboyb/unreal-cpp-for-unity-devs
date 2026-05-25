# Networking and Replication

Unity networking habits do not transfer directly to Unreal. Unreal has a built-in authority and replication model that shapes how gameplay code is written.

## Authority Model

### Unity Version

In Unity, networking choices vary a lot depending on the package or third-party solution.

### Unreal Version

In Unreal, the server is usually authoritative for important gameplay state.

### Key Difference

You often write code with explicit server, client, and owning-client responsibilities in mind.

## Server and Client Roles

| Concept | Meaning |
|---|---|
| Authority | The machine that owns the true gameplay state, usually the server. |
| Autonomous proxy | A client-controlled pawn on its owning client. |
| Simulated proxy | A replicated actor viewed on other clients. |

## `HasAuthority`

Use `HasAuthority()` to check whether an Actor is currently authoritative.

```cpp
if (HasAuthority())
{
    SpawnLoot();
}
```

This does not mean "am I the server?" in every abstract sense, but it is a common gameplay check on replicated actors.

## Replicated Properties

```cpp
UPROPERTY(Replicated)
int32 CurrentAmmo = 30;
```

Replicated properties must also be registered in `GetLifetimeReplicatedProps`.

## RPCs

Unreal supports remote procedure calls with `UFUNCTION` specifiers.

### Server RPC

```cpp
UFUNCTION(Server, Reliable)
void ServerFireWeapon();
```

### Client RPC

```cpp
UFUNCTION(Client, Reliable)
void ClientShowHitMarker();
```

### NetMulticast RPC

```cpp
UFUNCTION(NetMulticast, Unreliable)
void MulticastPlayImpactEffect();
```

## Reliable vs Unreliable

- `Reliable` should arrive, but use it carefully
- `Unreliable` is fine for frequent cosmetic updates where occasional loss is acceptable

## Replicated Gameplay Classes

| Class | Typical Network Role |
|---|---|
| `GameMode` | Server only |
| `GameState` | Replicated shared match state |
| `PlayerController` | Exists on server and owning client |
| `PlayerState` | Replicated per-player data |
| `Pawn` / `Character` | Often replicated gameplay avatar |

## Common Mistake

A common trap is trying to drive all gameplay from local client scripts, then expecting replication to "just sync it later". In Unreal, important state changes usually need a server-authoritative path from the start.

## Related Pages

- [Gameplay Framework](gameplay-framework.md)
- [Actors, Pawns and Characters](actors-pawns-and-characters.md)
- [Memory and Object Lifetime](memory-and-object-lifetime.md)
