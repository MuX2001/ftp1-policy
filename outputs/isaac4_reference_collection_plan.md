# Isaac Sim 4.5 reference collection

Purpose: establish a controlled visual and tactile diagnostic baseline for the
separate Isaac Sim 6 integration. These episodes are not training data and do
not run a learned policy.

## Collection scope

- Environment: `univtac-isaac4-baseline` only; Sim 6 is out of scope.
- Runner: `univtac4-install` tmux session (kept alive).
- Config: `isaac4_baseline_raw`.
- Tasks: `lift_bottle`, `lift_can`, `insert_HDMI`, `insert_hole`,
  `insert_tube`, `pull_out_key`, `put_bottle_in_shelf`.
- Per task: one successful scripted episode, seed search starting at zero.
- Stored modalities: head/wrist RGB and depth; left/right tactile RGB, marker,
  marker data, depth, and pose. Image encoding is disabled so HDF5 stores raw
  frames.

## Acceptance checks

For every produced HDF5 episode:

1. The expected visual and tactile datasets exist and are nonempty.
2. Head/wrist RGB and depth have matching temporal stages.
3. Both tactile pads have meaningful depth variation during contact stages.
4. A manifest records the episode path, shapes, dtypes, and contact/deformation
   summary for later Sim 6 comparison.

## Comparison rule

Compare like seeds and manipulation stages, not exact pixels. Renderer and
physics differences between Isaac Sim 4.5 and 6 are expected; loss of bilateral
tactile deformation/contact is the primary integration signal.
