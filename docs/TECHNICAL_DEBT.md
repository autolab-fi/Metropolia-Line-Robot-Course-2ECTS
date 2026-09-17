# Technical debt and release-readiness checklist

This document tracks work that must be completed before the 2 ECTS course is
treated as production-ready. It separates student delivery mode from technical
compatibility: a task may be assigned only in simulation, but its reference
program and APIs should still be checked on the physical robot.

## P0 — execution correctness and simulator/robot parity

### Validate every active assignment in both environments

Run the same trusted reference program against the simulator and the physical
Metropolia robot for every task in `lessons-list.json`. `Welcome` and `Sandbox`
need smoke tests; all 16 assessed tasks need full verification.

For each task, record:

- course, task, verifier, simulator, firmware, and robot-wrapper revisions;
- five simulator runs and five physical runs from a known initial pose;
- pass/fail result and returned score;
- executed API calls, stdout, and final stop state;
- elapsed execution time;
- final position and heading where movement is involved;
- ordered checkpoints and line-loss/recovery events for navigation tasks;
- representative Octoliner/encoder values for sensor tasks; and
- any reset, camera, queue, connection, or verifier failure.

Acceptance criteria:

1. The trusted program passes the intended verifier in both environments.
2. The robot always reaches a safe stopped state.
3. Simulator and hardware agree on command order and functional outcome.
4. Distance, heading, timing, encoder, and sensor differences stay inside a
   documented task-specific tolerance. Tolerances must be based on repeated
   measurements rather than one universal guessed value.
5. Instructions, starter code, simulator checks, and physical verification do
   not require contradictory constants or output text.

Create a parity report with one row per task. Do not mark a task ready from a
single successful run.

### Known calibration gaps

- `encoder_theory`: the current trusted program produces an encoder value
  outside the interval expected by the existing simulator check. Calibrate the
  motor model or correct the trusted program before enabling browser grading.
- `simple_line_follower`: calibrate the initial pose and ordered checkpoints to
  the Metropolia track before enabling browser grading.
- `test_drive`: run the full simulator-to-robot flow and review the physical
  verifier tolerance. Historical HAMK logs included technical failures in this
  introductory task, so infrastructure errors must not appear as student errors.
- `differential_drive`, `intro_to_octoliner`, `conditional_logic`, and
  `arrays_and_elif`: repeat physical and simulated baselines after every world,
  wrapper, firmware, or sensor-model change.

### Missing simulator verification

These active tasks have a physical verifier but are intentionally not exposed in
`simulation/manifest.json` yet:

- `encoder_theory` and `simple_line_follower` — calibration required;
- `proportional_control` and `adaptive_speed` — controller checks required;
- `art_of_debugging` and `hardware_safety_net` — deterministic code/runtime
  checks required; and
- `adaptive_racing` — simulator practice and final-challenge checks required.

The target modes are recorded in `curriculum-plan.json`. A task must not be
added to the simulation manifest until its trusted reference passes automated
browser tests.

## P1 — replace obsolete UI screenshots and external media

The following active lesson contains platform screenshots that should be
recaptured against the current Metropolia frontend:

- `lessons/module_1/mission_1.1.md`
  - `images/module-1/Interface1.png`;
  - `images/module-1/upload.gif`; and
  - the externally hosted course-9 image referenced from `api.ondroid.org`.

Additional active media requiring review:

- `lessons/module_3/mission_3.1.md` uses an opaque course-9 media URL;
- `lessons/module_3/mission_3.4.md` uses both an opaque course-9 media URL and
  an image from a third-party GitHub repository; and
- `images/course-info/` still contains inherited covers that must be checked for
  the final 2 ECTS title, current interface, Metropolia branding, and Mars theme.

For replacement screenshots:

1. Use the current production layout and Metropolia course branding.
2. Avoid personal information, tokens, queue identifiers, and live student code.
3. Capture the simulator selector, physical-robot submission path, output panel,
   and video panel at a consistent desktop resolution.
4. Store assets locally in this repository with descriptive filenames.
5. Replace opaque `/media/courses/9/...` and third-party links with repository
   assets so the course is independently reproducible.
6. Check legibility on desktop and mobile before merging.

## P1 — change the narrative from the Moon to Mars

The active course still contains Moon/Artemis language. At minimum, revise:

- `lessons/module_1/mission_1.1.md` — Artemis, Moon, lunar terrain vehicle;
- `lessons/module_1/mission_1.7.md` — geological/mineral route context;
- `lessons/module_3/mission_3.1.md` — lunar surface and Mission Control;
- `lessons/module_3/mission_3.4.md` — lunar mineral-vein survey;
- `lessons/module_3/mission_3.6.md` — Artemis rover wording;
- `lessons/module_4/mission_4.2.md` — LunarRover/Artemis telemetry examples;
  and
- `lessons/module_6/mission_6.2.md` — lunar crater and lunar facility.

Use one consistent Mars mission vocabulary across the course. Keep stable
`str_id` values for analytics and compatibility; change student-facing names and
text only. Review all of the following together:

- headings, introductions, objectives, assignments, and conclusions;
- starter templates and expected stdout strings;
- reference solutions and verifier messages;
- course cover images, diagrams, map labels, and alt text; and
- simulator world/robot labels visible to students.

Do not perform a blind Moon-to-Mars text replacement. Scientific context,
terrain descriptions, mission names, and images must remain internally
consistent, and any text used by an automated verifier must be updated in the
same change.

## P2 — release automation and regression protection

- Add a validator ensuring every lesson URL resolves to a repository file and
  every task has a matching physical verifier function.
- Add a validator comparing `lessons-list.json`, `curriculum-plan.json`, and
  `simulation/manifest.json` so implementation status cannot drift.
- Add trusted-reference regression tests for every enabled simulator task.
- Store structured failure categories: student code, behavioural check,
  verifier, robot/infrastructure, cancelled, and unknown.
- Store execution target (`simulation` or `robot`) and task/verifier version in
  attempt analytics so parity and learning outcomes can be compared later.
- Re-run the complete parity matrix after changes to firmware, the robot API,
  world geometry, motor calibration, sensor modelling, task instructions, or
  verification code.

## Definition of done

The course is ready for a pilot when all P0 items are closed, every active lesson
has passed content review, all student-facing Moon/Artemis references have been
converted to the agreed Mars narrative, obsolete screenshots have been
replaced, and the parity report has no unexplained simulator/robot divergence.
