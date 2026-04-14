# tour_guide_robot



## Overview 

### Robot Duties

* Navigates using a prebuilt map
* Visits landmarks in an optimized order
* Confirms arrival using AprilTags
* Ensures people are nearby at each stop before proceeding
* Returns to home base based on battery constraints
* Waits for human assistance when navigating doorways using AprilTags

## Modules

### Locomotion Controller

* Uses Nav2 for:
  * Global path planning
  * Path execution
  * Obstacle avoidance

* Accepts goal positions from Landmark Manager and navigates to them

### Landmark Manager

* Stores:
  * Landmark poses
  * Associated AprilTag IDs
  * Metadata (e.g., doorway, interaction behavior)

### AprilTag Scanner

* Uses `apriltag_ros`
* Detects tags at:
  * Landmarks
  * Doors
* Used for:
  * Landmark confirmation
  * Pose refinement
  * Door state detection
  
### Interaction Controller

* Handles:
  * Scanning and waiting for nearby people when at a landmark
  * Door-wait behavior
* Determines when:
  * Proceed through a doorway
  * Move to the next location

### Tour Deliberation Node

* High-level decision making:
  * Determine landmark ordering
  * Battery-aware planning
  * Continue tour vs return home​

## Sensors Used

* **LiDAR (RPLIDAR)** - Mapping, localization, obstacle detection
* **Camera (OAK-D)** - AprilTag detection
* **Encoders** - Odometry
* **Bumpers** - Collision detection

## Dependencies

* ROS 2
* Nav2
* Gazebo
* SLAM Toolbox
* apriltag_ros
* TF2

## Behaviors

* Human Detection
  * The robot performs a local scan at each landmark
  * Detects nearby objects not present in the static map using LiDAR
  * If an object is detected within a defined radius, it assumes a person is present
  * If no object is detected, the robot waits or skips after a timeout

* Door Detection
  * The robot aligns with a door using an AprilTag
  * While waiting, it continuously checks for the presence of the tag
  * If the tag is no longer visible, the robot assumes the door has been opened
  * The robot then proceeds through the doorway
