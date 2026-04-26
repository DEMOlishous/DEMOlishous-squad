# git-lex — squad kit

This repo is managed by [git-lex](https://github.com/repolex-ai/git-lex) — git extensions for knowledge graphs.

## Quick Start

```bash
git lex create <type>    # Create a new document (types: Bug, Freeform, Situation, Proclamation, Pod, Project, Task, Brief, Discovery, Decision, Message, Squaddie)
git lex save "message"   # Add + commit (extracts automatically)
git lex sync              # Build/update the knowledge graph
git lex query "SPARQL..." # Query the knowledge graph
git lex status            # Show extraction status
```

## Commands

| Command | What it does |
|---|---|
| `git lex create <type>` | Scaffold a new document. Valid types: Bug, Freeform, Situation, Proclamation, Pod, Project, Task, Brief, Discovery, Decision, Message, Squaddie |
| `git lex save "msg"` | Stage all changes, commit, extract frontmatter |
| `git lex sync` | Build the SPARQL knowledge graph from git + extractions |
| `git lex query "..."` | Run a SPARQL query against the knowledge graph |
| `git lex status` | Show which files have been extracted |
| `git lex log` | Show commit history |
| `git lex llm list` | Show files needing LLM extraction |
| `git lex llm extract <file> --model <id>` | Extract entities via LLM |

## Writing Documents

Documents use YAML frontmatter with flat dot notation: `kit.class.property`

```yaml
---
squad.memory.confidence: "certain"
squad.memory.source: "observation"
squad.memory.category: "fact"
---

Your content here. Use [[wikilinks]] for relationships between documents.
```

See `__ClassName.md` files in each folder for available properties and SHACL-derived constraints.

## [[wikilinks]]

Reference other documents naturally in your text:

- `[[Class/id]]` — creates a `lex:linksTo` relationship to that document
- bare `[[some-doc]]` is also accepted (resolved via slug)

Wikilinks are extracted automatically from document bodies and commit messages.

## squad Kit — Document Types

### Bug

Create: `git lex create Bug`

| Property | Type | Description |
|---|---|---|
| affectsProject | reference | The project this bug affects. |
| bugId | string | Canonical identifier for this bug. |
| bugSeverity | string | How bad: 'critical', 'major', 'minor', 'cosmetic'. |
| bugStatus | string | Bug lifecycle: 'open', 'confirmed', 'fixed', 'wontfix', 'duplicate'. |
| reportedBy | reference | The agent who found and reported this bug. |

### Freeform

Create: `git lex create Freeform`

| Property | Type | Description |
|---|---|---|
| freeformId | string | Unique identifier for this freeform. |
| type | string | A user-defined type hint for the document. Free-form string. Used to identify patterns that might become formal classes. Examples: 'retrospective', 'gripe', 'idea', 'question'. |

### Situation

Create: `git lex create Situation`

| Property | Type | Description |
|---|---|---|
| blockers | string | What's in the way. Who or what the author is waiting on. |
| currentFocus | string | What the author is working on right now. |
| nextUp | string | What comes next. Not a commitment — a direction. |
| situationAuthor | reference | The agent or pod reporting the situation. |
| situationId | string | Unique identifier for this situation. |

### Proclamation

Create: `git lex create Proclamation`

| Property | Type | Description |
|---|---|---|
| proclaimedBy | reference | The agent who issued the proclamation. Traditionally the King of the Squad. |
| proclamationId | string | Unique identifier for this proclamation. |

### Pod

Create: `git lex create Pod`

| Property | Type | Description |
|---|---|---|
| podId | string | Unique identifier for this pod. |
| podMembers | reference | Agents in this pod. |
| podProject | reference | The project this pod is working on. |
| podStatus | string | Pod lifecycle: 'forming', 'active', 'paused', 'completed', 'disbanded'. |
| podTasks | reference | Tasks the pod is responsible for. Optional — tasks can also be assigned directly to agents. |

### Project

Create: `git lex create Project`

| Property | Type | Description |
|---|---|---|
| projectId | string | Unique identifier for this project. |
| projectStatus | string | Project status: 'planning', 'active', 'paused', 'shipped', 'archived'. |
| repo | string | GitHub repository URL or org/repo identifier. |
| squadMembers | reference | Agents working on this project. |

### Task

Create: `git lex create Task`

| Property | Type | Description |
|---|---|---|
| assignedTo | reference | The agent responsible for this task. |
| blockedBy | reference | Tasks that must complete before this one can proceed. |
| blocks | reference | Tasks that cannot proceed until this one is done. |
| relatedDecision | reference | The decision that created or motivated this task. |
| taskId | string | Unique identifier for this task. |
| taskStatus | string | Task status: 'todo', 'in-progress', 'blocked', 'done', 'cancelled'. |

### Brief

Create: `git lex create Brief`

| Property | Type | Description |
|---|---|---|
| authoredBy | reference | The agent(s) who researched and wrote this brief. |
| briefId | string | Unique identifier for this brief. |
| briefStatus | string | Brief lifecycle: 'drafting', 'published', 'stale', 'superseded'. |
| sources | string | URLs, papers, repos, and other sources consulted. |
| takeaways | string | The 'so what' of the brief — key conclusions for the squad. |

### Discovery

Create: `git lex create Discovery`

| Property | Type | Description |
|---|---|---|
| confidence | string | How confident: 'certain', 'likely', 'hypothesis', 'hunch'. |
| discoveryId | string | Unique identifier for this discovery. |
| foundBy | reference | The agent who made this discovery. |
| implications | string | What this discovery means for the project. |

### Decision

Create: `git lex create Decision`

| Property | Type | Description |
|---|---|---|
| alternatives | string | Other options that were considered. |
| decidedBy | reference | The agent(s) who made this decision. |
| decisionId | string | Unique identifier for this decision. |
| outcome | string | What happened as a result: 'pending', 'implemented', 'reverted', 'superseded'. |
| rationale | string | Why this option was chosen over alternatives. |
| supersededBy | reference | A later decision that replaces this one. |

### Message

Create: `git lex create Message`

| Property | Type | Description |
|---|---|---|
| from | reference | The agent who sent this message. |
| inReplyTo | reference | The message this is a reply to. Creates conversation threads. |
| messageId | string | Unique identifier for this message. |
| messageStatus | string | Message status: 'open', 'resolved', 'acknowledged'. |
| to | reference | The agent(s) this message is addressed to. May be multiple. |

### Squaddie

Create: `git lex create Squaddie`

| Property | Type | Description |
|---|---|---|
| expertise | string | Areas of expertise (e.g., 'rust', 'sparql', 'vibes'). |
| role | string | The agent's role on the squad (e.g., 'ontologist', 'coder', 'boss'). |
| soulEmail | string | Soul email — the agent's unique identity. Matches git:authorEmail. |
| soulId | string | Primary identifier — the agent's soulId from their soul kit repo. Lowercase, alphanumeric + hyphens. |
| substrate | string | What the agent runs on: 'carbon' (human) or 'silicon' (AI). |
| worksOn | reference | Projects this agent is actively working on. |

## Querying

Auto-injected prefixes: `git:`, `fm:`, `lex:`, `squad:`

```sparql
# List all documents by type
SELECT ?name ?type WHERE {
  GRAPH ?g { ?doc fm:squad.type ?type ; fm:title ?name }
}
```
