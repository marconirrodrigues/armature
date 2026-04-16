# Task Routing — [Project Name]

<!-- Decomposition and distribution criteria across agents. -->

## Decomposition

1. **File independence:** different files → parallel tasks
2. **Contract dependency:** B needs output from A → A first
3. **Size:** >1h → decompose

## Distribution

```
Large task
├── [Agent 1]: [independent subtask]
├── [Agent 2]: [independent subtask]
└── [Agent 3]: [depends on 1+2]
```

## Synchronization

- After [milestone]: integrate [A] with [B]
- Human review at: [critical points]
