# Experiment Report Workspace

Workspace name: `{{WORKSPACE_NAME}}`
Variant: `experiment-report`
Focus: `{{EXPERIMENT_FOCUS}}`

This repository is a structured workspace for designing, running, and reporting on experiments and evaluations — hypothesis through data collection through analysis through final report.

## Directory Layout

- `design/` — experiment design documents. One markdown file per experiment, named in kebab-case (e.g. `prompt-length-vs-output-quality.md`). Defines research question, hypotheses, methodology, variables, controls, success criteria.
- `trials/` — raw trial data and run logs. Each trial run has its own subfolder: `trials/<experiment>/run-NN/`. Store inputs, outputs, configuration snapshots, and a `details.md` documenting exact conditions.
- `analysis/` — analysis outputs: statistical summaries, charts, comparison tables, intermediate notes. Organised by experiment.
- `reports/` — final experiment reports. Standalone markdown documents synthesising design + results + analysis into a narrative with conclusions.

## Design Document Format

```markdown
# Experiment: Title

**Version:** X.Y.Z
**Last updated:** YYYY-MM-DD

## Research Question
What specific question does this experiment answer?

## Hypotheses
- H1: primary hypothesis
- H2: secondary hypothesis

## Methodology

### Variables
- Independent: ...
- Dependent: ...
- Controlled: ...

### Procedure
Numbered steps for running one trial.

### Success Criteria
What counts as support or refutation of each hypothesis.

## Expected Outputs
What artifacts each run produces.
```

## Trial Run Format

Each `trials/<experiment>/run-NN/` should contain:

- `details.md` — timestamp, conditions, inputs, any deviations from the design.
- `inputs/` — input artifacts.
- `outputs/` — raw outputs.
- `config.json` or equivalent — machine-readable run configuration.

## Report Format

```markdown
# Report: Experiment Title

**Version:** X.Y.Z
**Run range:** run-01 through run-NN
**Report date:** YYYY-MM-DD

## Summary
One-paragraph finding.

## Methodology
Link to `design/<experiment>.md`.

## Results
Summary tables, charts (linked from `analysis/`).

## Analysis
Interpretation.

## Conclusions
Hypothesis outcomes, next steps.

## References
```

## Workflow

1. `/knowledge-documentation:new-page "Title" --type=design` — scaffold an experiment design.
2. Execute trials manually or via external tooling; drop artifacts under `trials/<experiment>/run-NN/`.
3. Run analysis; save outputs to `analysis/<experiment>/`.
4. `/knowledge-documentation:new-page "Title" --type=report` — scaffold the final report.
5. `/knowledge-documentation:cross-link` — link the report to its design and trials.
6. `/knowledge-documentation:version-doc` on substantive revisions.
7. `/knowledge-documentation:compile-handbook` to produce a combined multi-experiment report.
