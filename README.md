# ros2-dofbot-robotics-lab
ROS 2 robotics laboratory project exploring robotic arm control, forward and inverse kinematics, and pick-and-place simulation using the Yahboom DOFBOT SE.
ROS 2 Robotic Arm Laboratory | Kinematics and Control

Bakare Zainab Omodesola · Systems Engineering, University of Lagos · August 2026

Platform: Yahboom DOFBOT SE · Environment: ROS 2 Humble, Ubuntu 22.04, Python, RViz, MoveIt 2

Scope: Experiments 1–3 included practical laboratory work with the robotic arm; Experiments 4–5 were simulation-based. The report documents a simulated, not physically validated, pick-and-place sequence. This repository documents laboratory investigation using an existing software workspace, not a robot platform developed from scratch.

Photograph of DOFBOT robot 
Physical robotic arm used in the lab. Photograph does not demonstrate physical pick-and-place completion.

About the project

Five experiments examined the DOFBOT SE arm's physical structure, ROS 2 software architecture, forward and inverse kinematics, and simulated object manipulation. This documentation combines the hands-on practical sessions with analyses and verification against ROS 2 TF and MoveIt outputs reported in the laboratory report. The simulations and calculations use the robot's URDF geometry.

Experiments
Experiment	Setting	Focus	Evidence
1. Robot architecture and ROS 2	Practical + software tools	Joint/link identification, ROS 2 nodes/topics, joint-state monitoring	Physical-arm photo, communication graph, terminal output
2. Forward kinematics	Practical laboratory + software verification	Homogeneous transformations, home-pose and test-pose calculations	Model versus simulated TF results
3. End-effector position	Practical laboratory + software verification	Planar model in radial/vertical coordinates, wrist positioning	Planar FK results and terminal comparison
4. Inverse kinematics	Simulation	Elbow branches, joint limits, target reachability, MoveIt comparison	Solver and simulated joint-state results
5. Object reaching	Simulation	Reachability pre-check and hover → descend → close → lift → home	RViz simulated sequence

See experiments/ for short summaries and results/verification-summary.csv for selected figures transcribed from the report.

Selected results

- Forward kinematics: The report's full transformation model predicts a home-pose wrist height of approximately 0.447 m. A separately reported arm_link5 example shows Python FK (0.1327, -0.0008, 0.4178) m versus rounded ROS TF (0.133, -0.001, 0.418) m, an apparent difference of ~0.41 mm.
- Planar model: Reported comparisons with simulated TF range from approximately 1.7 to 2.1 mm for three configurations; the simplified model omits small fixed offsets present in the full URDF model.
- Inverse kinematics: For target (0.16, 0.00, 0.06) m and a 20° tool tilt, the elbow-A solution passed joint-limit checks while elbow-B failed. The report finds less than 0.0001 rad difference versus MoveIt's numerical solution for the tested valid target.
- Simulated picking: With (x, y) = (0.160, 0.000) m, hover z = 0.080 m, grasp z = 0.035 m and 22° tilt, the report records completion of a simulation sequence. Its physical pick attempt log remained pending.

Interpretation: These figures compare mathematical calculations and simulated transforms, not physical end-effector positioning accuracy. Some pose identifiers differ between report text, figure captions and summary tables; examples above are identified by coordinates and frame instead of ambiguous pose numbers.

Evidence gallery

Experiment 1: ROS 2 graph and joint states

ROS 2 communication graph 
Joint state subscriber output

Experiments 2–3: forward kinematics

Forward kinematics comparison 
Planar kinematics comparison

Experiment 4: inverse kinematics

Inverse kinematics solver output

Experiment 5: simulated pick-and-place

RViz pick sequence simulation

Tools and source attribution

The laboratory used the existing Yahboom DOFBOT ROS 2 workspace supplied as part of the course. The report documents the use of ROS 2 Humble, URDF descriptions, Python, ROS 2 CLI, RViz, TF and MoveIt 2.

Code provenance: My original workspace is no longer accessible. The report includes one complete joint_echo.py listing and names other scripts (fk_dofbot.py, fk_planar.py, ik_planar.py, goto_joints.py, pick_object.py), but their complete original files and authorship cannot currently be verified. No source scripts are included in this repository, and this documentation does not claim independent authorship of the supplied workspace or missing scripts.

Limitations

- Physical hardware interaction was part of Experiments 1–3, but the numerical verification values in this repository are from simulation, not physical metrology.
- Experiments 4–5 were simulation-based; the physical picking trial was not completed in the submitted report.
- Experiment 6 (trajectory planning) was described in the lab manual but not included in the completed report.
- The high-level /joint_states reflects commanded target angles, not independent encoder feedback.
- The course code is intentionally omitted pending confirmation: the report and manual show different codes.

Credits

- Course-provided laboratory manual, Control of Human and Robotic Arm.
- daveades/yahboom-robot-arm — existing ROS 2 workspace used for the coursework.
- Robot Operating System, ROS REP-103 (units and coordinate conventions).

Note: Figures are taken from my laboratory report. The repository is documentation of the learning and verification process; it is not a standalone runnable robot-control package.
