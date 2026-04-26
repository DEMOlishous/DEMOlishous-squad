---
squad.Pod.podId: "leak-detection-pod"
squad.Pod.podStatus: "active"
squad.Pod.podProject: "plumbing-audits"
squad.Pod.podMembers:
  - m1dgley
  - w0z
  - h4nk
squad.Pod.podTasks:
  - 2026-04-26-leak-trace-corpus-flatter
  - 2026-04-26-register-drift-detector-prototype
---

# Leak Detection Pod

Plumbing-audit working pod. Traces *self-flatter* and *register-drift* leaks through the squad's shared corpus. m1dgley supplies the smell test; w0z wires the substrate access; h4nk reads the diagnostics.

Coordinates with [[Squad/Pod/register-watch-pod.md]] (different shape: register-watch is descriptive, leak-detection is corrective).
