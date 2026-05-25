# UI with UMG

UMG is Unreal's main runtime UI system.

## Unity UI vs UMG

| Unity | Unreal | Notes |
|---|---|---|
| Canvas UI | UMG widget tree | Same broad purpose, different authoring workflow. |
| `MonoBehaviour` on UI objects | `UUserWidget` | Main UI class for runtime widgets. |
| Inspector references | `BindWidget` and reflected fields | Widget binding depends on matching names and Blueprint setup. |

## `UUserWidget`

Most runtime UI classes derive from `UUserWidget`.

```cpp
UCLASS()
class MYGAME_API UMyHUDWidget : public UUserWidget
{
    GENERATED_BODY()
};
```

## `BindWidget`

Use `BindWidget` when your C++ widget needs named child widgets from a Widget Blueprint.

```cpp
UPROPERTY(meta = (BindWidget))
TObjectPtr<class UTextBlock> ScoreText;
```

## Creating a Widget

```cpp
UMyHUDWidget* Widget = CreateWidget<UMyHUDWidget>(GetWorld(), WidgetClass);
```

## Adding a Widget to the Viewport

```cpp
if (Widget != nullptr)
{
    Widget->AddToViewport();
}
```

## Updating Text

```cpp
if (ScoreText != nullptr)
{
    ScoreText->SetText(FText::AsNumber(CurrentScore));
}
```

## Communicating Between UI and Gameplay Code

Common patterns include:

- player controller creates and owns the main HUD widget
- widget reads replicated values from player state or game state
- gameplay systems fire delegates that UI code listens to

## Common Mistake

A common trap is storing gameplay truth only inside the widget. UI should usually display or request data, not own the real game state.

## Related Pages

- [Blueprints and C++](blueprints-and-cpp.md)
- [Gameplay Framework](gameplay-framework.md)
- [Lifecycle and Events](lifecycle-and-events.md)
