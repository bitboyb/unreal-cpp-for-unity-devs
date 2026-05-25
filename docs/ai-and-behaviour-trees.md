# AI and Behaviour Trees

Unreal includes more built-in AI framework structure than many Unity projects use by default.

## Unity Scripted AI vs Unreal AI Framework

| Unity | Unreal | Notes |
|---|---|---|
| Script on NPC object | `AIController` plus Pawn/Character | Logic and controlled body are more clearly separated. |
| Custom decision code | Behaviour Tree | Common high-level decision system. |
| Shared blackboard data script | Blackboard | Stores AI working memory. |
| NavMesh agent | Navigation system and path following | Unreal nav is tightly integrated with AI controllers. |

## `AIController`

An `AIController` possesses a pawn the same way a player controller does.

It often handles:

- behaviour tree startup
- perception callbacks
- target selection
- move requests

## Behaviour Trees

Behaviour Trees define high-level decision flow using nodes such as:

- selectors
- sequences
- tasks
- decorators
- services

## Blackboards

Blackboards store AI state, such as:

- current target
- patrol point
- last known player location
- combat state

## Perception

Unreal AI Perception can detect stimuli such as sight and hearing.

This is often easier to scale than custom overlap checks on every NPC.

## Navigation Mesh

Unreal commonly uses a nav mesh volume for AI movement.

If AI will not move, check:

- nav mesh coverage
- possession
- movement component setup
- behaviour tree state

## C++ Integration Points

Common C++ entry points include:

- custom `AIController` classes
- custom behaviour tree tasks
- perception callbacks
- helper functions on the controlled pawn

## Common Mistake

A common trap is putting all AI state on the pawn and skipping the controller layer. In Unreal, controller and pawn separation is often worth keeping.

## Related Pages

- [Actors, Pawns and Characters](actors-pawns-and-characters.md)
- [Gameplay Framework](gameplay-framework.md)
- [Glossary](glossary.md)
