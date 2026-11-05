# Model and Dependency Licence Register

This file is intentionally a register, not a blanket assertion that models are free.

For every model, runtime, library and container added, record:

| Field | Required value |
|---|---|
| Name | Exact project/model |
| Version/revision | Exact tested version or commit |
| Official source | Official repository or publisher |
| Licence | Exact licence identifier and link |
| Commercial use | Allowed / restricted / prohibited / unclear |
| Redistribution | Conditions |
| Attribution | Required text, if any |
| Model weights | Source and checksum |
| Hardware | Tested GPU, VRAM, RAM |
| Validation date | YYYY-MM-DD |
| Decision | Approved / blocked / needs legal review |

Rules:
- Do not infer licence from a model family name.
- Code licence and model-weight licence may differ.
- Training data and output terms may have separate conditions.
- “Open weights” is not synonymous with OSI open source.
- If terms are ambiguous, mark `needs legal review` and disable commercial production use.