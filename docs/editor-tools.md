# Editor Tools

Unreal has several ways to build editor-side workflows for content teams and technical designers.

## Unity Custom Inspectors vs Unreal Editor Tooling

| Unity | Unreal | Notes |
|---|---|---|
| Custom inspector | Custom details panel | Editor UI customization for properties and tools. |
| Editor window | Editor Utility Widget | Fast way to build editor-facing UI tools. |
| Menu command / batch script | Commandlet | Useful for automation and headless tasks. |
| Package / extension | Plugin | Standard way to distribute editor tools and code. |

## Editor Utility Widgets

Editor Utility Widgets are one of the quickest ways to build a custom Unreal editor tool.

They work well for:

- content batch operations
- level setup helpers
- data cleanup tools
- designer-facing utility panels

## Blutilities

Blutility is the older term many people still use for editor utility scripting features. You may still see it in discussions or older examples.

## Commandlets

Commandlets are command-line style Unreal tasks used for automation.

Examples:

- data validation
- asset processing
- batch import or export steps

## Custom Details Panels

When a simple utility widget is not enough, you can extend the editor UI for specific classes with custom details panels.

This is closer to advanced Unity editor extension work.

## Plugins

Plugins are the normal way to package reusable editor tooling, runtime code, or both.

## When to Build Editor Tools

Build a tool when a repeated manual task is:

- slow
- error-prone
- done by multiple people
- difficult to standardize without automation

## Common Mistake

A common trap is solving a recurring content workflow with a long README checklist instead of a small editor tool. If the team repeats the same clicks every day, a tool may be worth it.

## Related Pages

- [Blueprints and C++](blueprints-and-cpp.md)
- [Version Control](version-control.md)
- [Glossary](glossary.md)
