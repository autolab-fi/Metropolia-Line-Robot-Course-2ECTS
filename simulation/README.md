# Browser simulation configuration

`manifest.json` contains only simulation checks that are currently enabled for
the 2 ECTS course. Physical verification remains in `verifications/` and is
executed by the lab worker.

The Metropolia world and robot wrapper are shared with the existing Metropolia
course. Task identifiers are preserved from that course so the same simulator
checks and physical verifiers can be reused.

## Execution modes

- `simulation-only`: the assignment is completed in the browser simulator.
- `simulation-and-lab`: the student runs the code in simulation and on the
  physical robot.
- `simulation-optional`: an ungraded practice workspace.
- `lab-only`: physical-robot verification; these tasks are omitted from this
  manifest until a simulator check is ready.

The enforced mode is stored with the assignment in `../lessons-list.json`.
Modes in this manifest must match it for every simulator-enabled task.

`test_drive` is the first hybrid assignment. The student uses exactly the same
program in both environments; no quiz or written response is required.

## Pending simulator work

The following active course tasks intentionally remain absent from the manifest
until their browser checks are implemented or calibrated:

- `encoder_theory` — the current trusted program and simulated encoder interval
  do not yet agree.
- `simple_line_follower` — start pose and checkpoints must be calibrated to the
  Metropolia track.
- `proportional_control` and `adaptive_speed` — controller checks are planned.
- `art_of_debugging` and `hardware_safety_net` — deterministic code checks are
  planned.
- `adaptive_racing` — simulation practice is planned; final validation remains
  on the physical robot.

Target modes and implementation state are tracked in `../curriculum-plan.json`.
Do not expose a planned simulator mode in this manifest until its trusted
program passes the browser checks.
