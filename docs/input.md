# Input

Unreal Engine 5 projects usually use Enhanced Input rather than the older input binding system.

## Unity Input System vs Unreal Enhanced Input

| Unity | Unreal | Notes |
|---|---|---|
| Input Action asset | `UInputAction` | Represents an input concept such as Move or Jump. |
| Input Action map | Mapping context | Groups bindings that can be added or removed at runtime. |
| Player input component | Enhanced Input component | Used for binding actions to functions. |
| Player input setup script | Player controller or character setup | Controllers often manage mapping context ownership. |

## Input Actions

An input action describes what you want to detect, such as movement or firing.

```cpp
UPROPERTY(EditDefaultsOnly, Category = "Input")
TObjectPtr<class UInputAction> JumpAction;
```

## Mapping Contexts

A mapping context groups related bindings.

Examples:

- on-foot controls
- vehicle controls
- menu navigation

You can add and remove contexts at runtime.

## Player Controller Role

The player controller often owns player-specific input setup because it survives pawn swaps more naturally than the pawn itself.

That said, many sample projects bind movement on the character. Both patterns appear in real projects.

## Character Input Binding

```cpp
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    if (UEnhancedInputComponent* EnhancedInput = Cast<UEnhancedInputComponent>(PlayerInputComponent))
    {
        EnhancedInput->BindAction(JumpAction, ETriggerEvent::Triggered, this, &ACharacter::Jump);
    }
}
```

## Adding a Mapping Context

```cpp
if (APlayerController* PC = Cast<APlayerController>(GetController()))
{
    if (ULocalPlayer* LocalPlayer = PC->GetLocalPlayer())
    {
        if (auto* InputSubsystem = LocalPlayer->GetSubsystem<UEnhancedInputLocalPlayerSubsystem>())
        {
            InputSubsystem->AddMappingContext(DefaultMappingContext, 0);
        }
    }
}
```

## Common Mistake

A common trap is binding input on an object that is not actually possessed by the local player. In Unreal, possession and controller ownership matter.

## Related Pages

- [Actors, Pawns and Characters](actors-pawns-and-characters.md)
- [Lifecycle and Events](lifecycle-and-events.md)
- [Gameplay Framework](gameplay-framework.md)
