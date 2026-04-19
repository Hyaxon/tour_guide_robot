# tourbot_mission

## Purpose
Implements high-level decision making and interaction logic for the tour.

## Contents
- Nodes:
  - tour_deliberation_node: selects landmarks and manages mission flow
  - interaction_controller: handles waiting, scanning, and door logic

## How it’s used
- Sends navigation goals to Nav2
- Receives input from sensors and AprilTag detection
