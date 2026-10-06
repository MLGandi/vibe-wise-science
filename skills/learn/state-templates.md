# Local state templates

Create only these three files in the chosen project's `.vibe-wise-science/`.
Use the directory selected by SKILL.md.
Replace bracketed values with actual evidence or “Not specified.” Keep the two
status lines unformatted and near the top; the restoration hook reads them.
Do not replace existing state with a fresh template.

## profile.md

```markdown
# Learner Profile

Learning mode: active
Onboarding: complete

## Project
Situation: [New / Existing / Known / Reproduce a paper]
Investigating: [research question or project purpose]
Codebase familiarity: [answer]
Learning scope: [whole project / parts we touch / mixed]

## Background
Field: [Psychology / NeuroAI / Machine learning / mix / other]
Methods background: [Beginner / Intermediate / Advanced, or Not specified]
Programming: [Beginner / Intermediate / Advanced, or Not specified]
Tool familiarity: [per-tool levels if given; otherwise Not specified]

## Goals
Primary: [answer]
Capability goal: [optional answer]

## Preferences
Checkpoint frequency: Normal
Question style: Open-ended
Code explanations: Brief
Implementation style: AI writes code

## Strong Concepts
No demonstrated understanding recorded yet.

## Developing Concepts
None recorded yet.

## Revisit
None recorded yet.
```

## progress.md

```markdown
# Learning Progress

No learning events recorded yet.
```

As learning occurs, add a `## Topic` with concise bullets under Introduced,
Demonstrated understanding, and Needs reinforcement. Record reasoning evidence,
not quotations of a whole exchange. Research goals and hoped-for results establish
requirements; they aren't evidence of methodological understanding. Keep
learner-proposed reasoning distinct from concepts Claude explained. For method
decisions, record the chosen method, the learner's justification in their own terms,
alternatives actually discussed, and which assumptions were checked and how.
Consolidate repeated entries. Keep each topic independently readable so it can be
loaded without the whole file.
While waiting on a checkpoint, keep a short `## Pending decision` section
with the proposed approach and what reply is awaited. Remove it once resolved.
Include the checkpoint's decision name and stage: awaiting reasoning, method choice,
choice confirmation, implementation approval, or interpretation. Record confirmed
choices in the map without claiming they are implemented. Keep any proposed coding
scope explicit. Confirmation covers only the proposal presented. Don't append
unmentioned steps, parameters, undiscussed alternatives, or reasons to the chosen
plan. Mark unresolved details unknown and Claude's suggestions proposed; never
attribute them to the learner. Never record participant-level or identifiable data.

## project-map.md

```markdown
# Project Map

## Research Question
[Question, hypotheses or predictions, and what result would count as support or
against. Not stated yet, if unknown.]

## Data
[Source, unit of observation, structure (trials, participants, stimuli, sessions;
nesting and repeated measures), sample size, key variables and units, provenance,
and privacy or consent constraints. Unknown when unverified. Structure only; no
participant-level records.]

## Pipeline
[Compact text diagram with labeled arrows: data → preprocessing → analysis or
model → outputs, with supporting file paths. Mark unknowns and distinguish proposed,
chosen, and implemented steps. Reflect the learner's model refined together, or
verified existing code; don't fill missing steps with assumed designs.]

## Methods
[Each step's method, its status (proposed / chosen / implemented), and the
learner's justification once confirmed.]

## Assumptions
[What each method assumes, and whether it has been checked: how, and with what result.]

## Validation
[Simulated-data recovery, null or permutation baselines, noise ceilings,
cross-validation scheme, leakage checks, seed variance. Planned versus run, with results.]

## Reproducibility
[Environment files, seeds, data versions, and commands verified in the repository.]

## Unknowns
[Unresolved choices and what needs inspection: measures, exclusions, methods,
validation, tools, and compute.]
```
