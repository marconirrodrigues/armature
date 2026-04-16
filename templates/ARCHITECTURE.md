# Architecture — [Project Name]

<!-- Dependency layers and module boundaries. Update as the system evolves. -->

## Layers

<!-- Dependencies flow ONLY downward. -->

```
[UI / Routes]
       ↓
[Services / Use Cases]
       ↓
[Data / Repository]
       ↓
[Types / Config]
```

## Modules

| Module | Responsibility | Depends on | Does NOT depend on |
|--------|---------------|------------|--------------------|
| [module] | [what it does] | [allowed] | [prohibited] |

## Integration Points

- [where modules meet — pay attention in code review]
