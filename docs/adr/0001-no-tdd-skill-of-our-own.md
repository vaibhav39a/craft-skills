# No TDD skill of our own

The obvious lineup for a craft-skills repo includes a TDD skill — the old repo shipped `craft-tdd`, and the improvement plan's first draft kept it. We ship none, deliberately: the ecosystem already has good TDD-loop skills (e.g. mattpocock/skills `tdd`), and this repo's evaluation found its effort had gone predominantly into commodity work while its differentiators starved. The loop is commodity; the one behavior that was ours — naming the cycle violation as it forms ("that's **Big-step green**") — is surfacing behavior, so it lives in `craft-coach` and its TDD concept files, which ride along with whatever tdd skill is driving.

Considered: keeping a self-contained ~50-line `craft-tdd` (no external dependency, one-stop install). Rejected because it duplicates a commodity, dilutes the repo's identity as *the surfacing layer*, and re-opens the concept-duplication problem (a second skill needing the TDD concepts inline).

Consequence: users who want the full experience install an ecosystem tdd skill alongside `craft-coach`; the README says so explicitly. Revisit if the ecosystem's tdd skills disappear or drift incompatibly.
