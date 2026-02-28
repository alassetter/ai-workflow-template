# Workflow Diagram

See setup and operational details in [instructions.md](/Users/marlin/Development/ai-workflow-template/instructions.md).

```mermaid
flowchart TD
    A["Start Session"] --> B{"Exactly one active feature<br/>in workflow/planning/active/?"}
    B -- "No (0)" --> C["Select feature from backlog<br/>and activate it"]
    B -- "No (2+)" --> D["Stop and resolve<br/>single-flight violation"]
    B -- "Yes (1)" --> E["Read active feature and related ADRs"]

    C --> E
    E --> F{"Architectural change needed?"}
    F -- "Yes" --> G["Create/Update ADR<br/>workflow/decisions/adr/"]
    G --> H["Approve/align ADR"]
    H --> I["Implement scoped work"]
    F -- "No" --> I

    I --> J["Run validation and CI checks"]
    J --> K["Write checkpoint<br/>workflow/journal/"]
    K --> L{"Feature complete?"}
    L -- "No" --> I
    L -- "Yes" --> M["Set Completed date"]
    M --> N["Move feature to<br/>workflow/planning/archive/"]
    N --> O["Log milestone<br/>workflow/milestones/"]
    O --> P["Activate next backlog feature"]
```

## Artifact Flow

```mermaid
flowchart LR
    A["workflow/templates/FEATURE.md"] --> B["workflow/planning/backlog/FXXX-*.md"]
    B --> C["workflow/planning/active/FXXX-*.md"]
    C --> D["workflow/planning/archive/FXXX-*.md"]
    C --> E["workflow/journal/YYYY-MM-DD-*.md"]
    F["workflow/templates/ADR.md"] --> G["workflow/decisions/adr/ADR-XXX-*.md"]
    H["workflow/templates/GOLDEN_CONVERSATION.md"] --> I["workflow/decisions/golden/GC-XXX-*.md"]
```

Back to the implementation guide: [instructions.md](/Users/marlin/Development/ai-workflow-template/instructions.md).
