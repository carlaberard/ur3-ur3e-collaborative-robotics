# Technical and safety notes

The `.script` files are archived academic robot programs and are **not independently tested** by this repository preparation workflow.

1. **Hardware-specific poses.** Original hard-coded joint configurations and Cartesian poses are lab-specific. Establish a safe workspace and validate every approach, pickup and placement pose before running them on any robot.
2. **Robot supervision.** Use qualified supervision, the applicable robot safety configuration, reduced speeds in initial trials, and accessible emergency stops.
3. **RG2 gripper.** The UR3e script calls `rg_grip` and `rg_payload_set`; this depends on the correct RG2 installation and URCap API availability.
4. **Relay required.** A compatible Python-based PC message relay is not included. Both robot programs call `socket_open()` to the relay at `PC_IP:8080`.
5. **Pose rotation caveat.** Adding pi to `pose[5]` changes a rotation-vector component and should not be assumed equivalent to a rotation around the tool's own Z axis in arbitrary poses. Validate rotation geometry prior to physical execution.
6. **Communication faults.** Both programs require expected incoming messages, but do not fully implement retries, coordinated failure recovery, or guaranteed acknowledgements for outgoing messages.
7. **Evidence.** The lab report describes testing/corrections and contains photographs and workflow diagrams, but does not provide a machine-readable run log or independent video validation. Descriptions should not imply more verification than the source supports.
8. **Educational use only.** The program is not a safety-rated collaborative control or clinical robotic system.
