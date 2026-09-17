# Introduction to Mobile Robotics @ Metropolia — 2 ECTS

This repository is the independent 2 ECTS course track for the Metropolia
line-following robot. It is derived from the existing Metropolia/HAMK course,
but has its own lesson list and can be developed without changing the currently
deployed course.

## Course shape

- Workload: 2 ECTS / 54 hours.
- 16 assessed programming assignments.
- `Welcome` and `Sandbox` are orientation activities worth zero points.
- No quizzes or short-answer tests are included.
- Deterministic Python exercises use the browser simulator.
- Hardware milestones use the same code in simulation and on the real robot.
- The final adaptive line-following challenge is validated on the real robot.

The course starts with an early hardware experience. In `Test Drive`, the
student runs the program in the simulator and then executes the same program on
the physical robot. The physical check should grade safe forward movement,
stopping, and successful completion rather than exact final coordinates.

## Workload budget

| Area | Hours |
| --- | ---: |
| Orientation and playground | 2 |
| Python and robot motion | 12 |
| Motors and sensors | 12 |
| Line-following control | 12 |
| Debugging and safety | 11 |
| Final robot challenge | 5 |
| **Total** | **54** |

## Repository files

- `course-info.json` — platform-facing course metadata.
- `lessons-list.json` — the active 2 ECTS module and assignment list.
  Each assignment declares its enforced `executionMode`.
- `curriculum-plan.json` — intended execution environment and implementation
  status for each assignment.
- `docs/TECHNICAL_DEBT.md` — content, screenshot, calibration, and
  simulator/robot parity work required before the pilot.
- `simulation/manifest.json` — simulation modes and checks that are currently
  implemented.
- `lessons/` — lesson content inherited from the existing course.
- `verifications/` — physical-lab verification code.

Task string identifiers are intentionally preserved so existing lesson content,
verification code, and historical analytics remain comparable.

## Implementation status

The introductory simulator tasks, the first hybrid robot tasks, encoder work,
sensor exercises, and the simple line follower already have browser checks.
Simulator checks for proportional/adaptive control, debugging, safety, and the
final challenge remain planned and are not exposed as implemented in the
simulation manifest.

`simulation-and-lab` makes both execution targets available and requires a
successful simulator attempt before physical-robot verification. Tasks whose
simulator checks are still planned or need calibration remain `lab-only` in
`lessons-list.json`; their intended future modes stay in `curriculum-plan.json`.
