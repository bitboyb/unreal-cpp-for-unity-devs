# Glossary

This glossary lists important Unity and Unreal terms used across the guide.

| Term | Engine | Meaning |
|---|---|---|
| Actor | Unreal | A level-placeable or spawnable gameplay object. |
| AIController | Unreal | A controller that possesses and directs AI pawns. |
| Blackboard | Unreal | Shared AI working memory used by Behaviour Trees. |
| Blueprint | Unreal | A reflected asset class that can define components, defaults, and visual scripting logic. |
| Character | Unreal | A Pawn subclass with built-in character movement support. |
| Component | Both | A reusable part that adds behaviour, data, or structure to another object. |
| Controller | Unreal | An object that possesses and directs a Pawn. |
| Data Asset | Unreal | An asset used to store structured data, often as a designer-editable alternative to code-only data containers. |
| Delegate | Unreal | Unreal's callback and event binding system. |
| Details Panel | Unreal | The editor panel used to inspect and edit reflected properties. |
| Enhanced Input | Unreal | Unreal Engine 5's modern input framework. |
| FName | Unreal | A lightweight name type used for identifiers and lookups. |
| FString | Unreal | Unreal's general-purpose string type. |
| FText | Unreal | Unreal's user-facing text type, designed for localisation. |
| GameMode | Unreal | The server-side class that defines rules, default classes, and match flow. |
| GameObject | Unity | A scene object that holds components. |
| GameState | Unreal | A replicated class that stores shared match state for clients. |
| Garbage Collection | Unreal | Engine-managed cleanup of unreachable `UObject` instances. |
| Level | Unreal | A map asset that contains placed actors and world content. |
| Mapping Context | Unreal | A group of input bindings in Enhanced Input. |
| MonoBehaviour | Unity | The base class commonly used for Unity gameplay scripts. |
| Pawn | Unreal | A possessable Actor, usually controlled by a player or AI controller. |
| Perforce | Both | A version-control system commonly used by larger Unreal teams. |
| PlayerController | Unreal | The class that represents player input and possession logic. |
| PlayerState | Unreal | A replicated class that stores per-player match data. |
| Reflection | Unreal | The engine system that exposes C++ classes, properties, and functions to the editor, Blueprints, serialization, and networking. |
| Scene | Unity | A collection of GameObjects loaded together. |
| Soft Reference | Unreal | An asset reference that can be loaded later instead of forcing an immediate hard dependency. |
| TArray | Unreal | Unreal's dynamic array template. |
| TObjectPtr | Unreal | A UE5 pointer wrapper commonly used for reflected `UObject` member references. |
| UFUNCTION | Unreal | A macro that exposes a function to Unreal systems such as Blueprints or RPCs. |
| UHT | Unreal | Unreal Header Tool, which processes reflected headers before C++ compilation. |
| UMG | Unreal | Unreal Motion Graphics, Unreal's main runtime UI system. |
| UObject | Unreal | The base class for many engine-managed objects. |
| UPROPERTY | Unreal | A macro that exposes a member variable to Unreal systems. |
| World | Unreal | The runtime world context that owns actors and gameplay state. |
