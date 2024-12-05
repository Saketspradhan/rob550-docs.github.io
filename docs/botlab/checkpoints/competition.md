---
layout: default
title: Competition
nav_order: 6
parent: Checkpoints
grand_parent: Botlab
last_modified_at: 2024-11-05 16:37:48 -0500
---

**Update 11/5/24:** Change competition events as forklift is no longer used.

<a class="image-link" href="/assets/images/botlab/checkpoints/doge-meme.png">
<img src="/assets/images/botlab/checkpoints/doge-meme.png" alt=" " style="max-width:250px;"/>
</a>

## Contents
* TOC
{:toc}

## Event 1: Speed Run [300 points max]

You will complete two runs in total, one of which is judged for accuracy and the second which is judged for speed.

For the first run, make a circuit around a convex arena by driving the path given to you. Do this while running SLAM to make a map of the arena. Return to the starting pose. You are judged based on the final error in pose and your map quality. Save an image of your map and upload the image to Google Drive.

For the second run, drive quickly around the path two times. You are judged on the speed to complete the run. For this run, you will not be judged based on your final error, but your ending pose must be close enough to the start that you are still partially on the starting piece of paper. If your final position is beyond that then you will receive no points for the speed run section.

Error in pose after mapping:
- 100 points: < (3 cm, 3 cm, 15°)
- 75 points: < (5 cm, 5 cm, 15°)
- 50 points: < (10 cm, 10 cm, 30°)
- 25 points: < (20 cm, 20 cm, 45°)

Map quality: [+100, +50, +25] for [Excellent, Good, OK] quality

Timed run:
- 100 points: 50s
- 75 points: 80s
- 50 points: 100s
- 25 points: 200s

The thresholds will be determined by the actual times on the first day of competition.


## Event 2: Maze Explorer [400 points max]

From the starting position, explore the maze and make a map of the environment. Then return to the start location/pose.

For partial credit:
- You may choose to use botgui for manual exploration of the map via right-clicking (using A* algorithm), but note that this will not earn you points for autonomous navigation.
- Alternatively, you can operate the bot manually (tele-op) to construct the map. In this case, points will be awarded based on the map's quality.

**Cone challenge:** If you choose to, we will place 3 randomly colored cones (no duplicates) in the maze. After mapping the environment, you will navigate to the cones in rainbow order (red first) before returning to the start.

Points:
- [+200, +150, +100, +50] points for returning to start pose with error limit:
    - 200 points: < (3 cm, 3 cm, 15°)
    - 150 points: < (5 cm, 5 cm, 15°)
    - 100 points: < (10 cm, 10 cm, 30°)
    - 50 points: < (20 cm, 20 cm, 45°)
- [+100, +50, +25] for map quality [Excellent, Good, OK] regardless of finishing
- +100 points for completing the cone challenge
- 25% deduction for using your A* path planner but using click to drive instead of full autonomy
- 50% deduction for using teleop

## Event 3: Warehouse [600 points max]

Below is an example of what the warehouse arena will look like.

<a class="image-link" href="/assets/images/botlab/checkpoints/competition.png">
<img src="/assets/images/botlab/checkpoints/competition.png" alt=" " style="max-width:400px;"/>
</a>

The purpose of this event is to locate Apriltag crates and cones and move the crates to designated drop-off zones.

### Setup

**All Levels**

* 3 Apriltag crates with cones on top of them will be placed in random places in the warehouse
  * Crate cone colors: Red or Green, randomly assigned
  * The Apriltags will have unique IDs
  * The crates will be placed with enough space around them to complete the tasks
* 2 cones will be placed in fixed places in the warehouse, marking dropoff zones
  * Dropoff cone colors: Blue and Yellow


**Level 1 and 2**

* The robot will be placed at a fixed position

**Level 3**

* The robot will be placed at an unknown position

### Tasks

**Level 1**

* Locate the Apriltags and cones. After finding all the Apriltags and cones, print out the position of each to the terminal. Your final printout must display the Apriltag ID (if applicable), cone color, and crate position for each detection.
  * A crate location is defined to be the **center** of the crate, **not the side** where the Apriltag is. The output of the Apriltag detector is the centroid of the Apriltag, which is not what we are after! For maximum accuracy you must find the center of the crate given the Apriltag position and orientation.
  * The Apriltag crates have 2 IDs. Printing out either one is fine. However, if you print out both on separate lines, they will be treated as two separate detections and count against you.
  * Example line format: `Pos: (14.4, 10.0), ID: 1 & 2, Color: Red`
* Then, drive close to an Apriltag with a red cone on top of it. Running into the Apriltag is allowed.
* The origin is defined to be the piece of paper where you start.

**Time limit:** 2 minutes

Points:

* [+20, +15, +10] points for each Apriltag/cone position printed out with location error:
  * 20 points: < (2 cm, 2 cm)
  * 15 points: < (5 cm, 5 cm)
  * 10 points: < (15 cm, 15 cm)
  * No points for correct position but wrong ID or color
  * -10 points per false positive detection, capped at -30 points
* [+100, +50] points for the final distance to Apriltag
  * 100 points: < 5 cm away from the Apriltag
  * 50 points: < 20 cm away
  * No points for > 20 cm away
* 50% deduction for using teleop or click to drive
* Your Apriltag/cone detection and localizing must be fully autonomous. You may choose when to print out the detections for grading.

**Level 2 and 3**

* Explore the area and locate each Apriltag crate and dropoff cone. After you have determined the positions, print out the detections as in Level 1.
* Then, move each Apriltag crate to a drop-off zone marked by a cone.
  * Apriltags with **red** cones on top of them go to the **yellow** drop off cone
  * Apriltags with **green** cones on top of them go to the **blue** drop off cone
* We will provide you with the 3D printed forks that you will attach to your bot and use to move the Apriltag crates
* The origin is defined to be the piece of paper where you start in Levels 1 and 2.

**Time limit:** 10 minutes

Points:

* [+50, +30, +20] points for each Apriltag/cone position printed out with location error:
  * 50 points: < (2 cm, 2 cm)
  * 30 points: < (5 cm, 5 cm)
  * 20 points: < (15 cm, 15 cm)
  * No points for correct position < (15 cm, 15 cm) but wrong ID or color
  * -10 points per false positive detection, capped at -30 points
  * **Level 3:** +150 points for correctly printing out all positions in the global reference frame
* +100 points for each Apriltag moved to the correct drop-off zone, < (15 cm, 15 cm) away from the cone
* 50% deduction for driving around using teleop or click to drive
* Your Apriltag/cone detection and localizing must be fully autonomous

Hint for Level 3: Make a map of the warehouse yourself, then during the competition pre-load that map and use your SLAM in localization only mode to determine your initial position.
