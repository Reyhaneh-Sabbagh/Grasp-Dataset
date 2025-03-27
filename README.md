## Dataset for grasping objects
Hand and finger motion tracking data for 29 adults. Three different experiments (Tasks) were conducted as detailed below. In all three experiments, users should reach the objects and then perform an action.
Each participant tries the experiment in two trials. Objects are located in one of two positions, 30 cm to the right or left side of the participant.
These experiments were conducted by Dimitar Valkov.

## Structure
The dataset has the following structure:

    dataset\
	    grasped_raw\
		    Task<taskID>_Grasped_User<UserID>.csv
		grasped_features\
		    Task<taskID>_Grasped_User<UserID>.csv
	    reaching_raw\
		    Task<taskID>_Reaching_User<UserID>.csv
	    reaching_features\
		    Task<taskID>_Reaching_User<UserID>.csv

- All files are in CSV format. Each file contains all trials for one paricipant and task (s. below).
- The folder `reachung_raw` contains the motion tracking data for the *reach-to-grasp (R2G)* phase for all participants, objects, and actions in the three experiment tasks.
- The folder `grasped_raw` contains the raw motion tracking data from the moment the participant first touched the object to the moment he/she released or lifted it from the surface.
- The folder `reaching_features` contains the hand and wrist motion velocity, as well as the thumb-finger aperture for the *R2G* phase.
- The folder `grasped_features` contains the hand and wrist motion velocity, as well as the thumb-finger aperture from the moment the participant first touched the object to the moment he/she released or lifted it from the surface.

## Tasks
- *Task 1*: The participant had to reach out and grasp one of the *real* objects and perform an action with it. The combination of object and actions is as follows:

| Action Name     | bottle     | cup   | knife | pen   |
|-----------------|------------|-------|-------|-------|
| non-use         | move       | move  | move  | move  |
| primary use     | pour       | drink | cut   | write |
| secondary use   | drink      | pour  | poke  | poke  |

- *Task 2*: The participant had to reach out and either *grasp*, or *touch*, or *push* one of the *synthetic* objects. The synthetic objects were named: *bar* - a high prismatic object, *box* - a medium sized cube, *dice* - a small cube, *plank* - a 2cm thin plank.

- *Task 3*: The participant had to reach out and *grasp* one of the *synthetic* objects and perform an action with it. The actions were named: *center* - place the object precisely at the predefined position; *somewhere* - place the object somewhere on the table, *hold* - hold the object for 2 seconds above the table, and *throw* - throw the object in a (trash)bin beneath the table.

## Variables
All files in the folders `grasped_raw` and `reaching_raw` have the following variables:
| Name             | Type       | Unit | Description                                                                 |
|------------------|------------|------|-----------------------------------------------------------------------------|
| `userID`         | `[int]`    |  --  | The user ID. Note that these are not consecutive numbers.                   |
| `object`         | `[string]` |  --  | The target object.                                                          |
| `side`           | `[string]` |  --  | The position (left or right) of the target object.                          |
| `action`         | `[string]` |  --  | The action to be performed.                                                 |
| `trialID`        | `[int]`    |  --  | The trial ID can be 0 or 1.                                                 |
| `phase`          | `[string]` |  --  | The motion phase can be `Reaching` or `Grasped`                             |
| `frameID`        | `[int]`    |  --  | The frame ID starts at 0 for each trial. Thus the first frame in the `Reaching` phase will be 0, and the first frame in `Grasped` phase will be the last frame of the corresponding reaching phase + 1                    |
| `frameTimeStamp` | `[double]` |  ms  | The frame time in milliseconds since the beginning of the trial.            |
| `px1`            | `[double]` |  cm  | The x-coordinate of sensor S1                                               |
| `py1`            | `[double]` |  cm  | The y-coordinate of sensor S1                                               |
| `pz1`            | `[double]` |  cm  | The z-coordinate of sensor S1                                               |
| `px2`            | `[double]` |  cm  | The x-coordinate of sensor S2                                               |
|       ...        |     ...    |  ... | ...                                                                         |
| `pz15`           | `[double]` |  cm  | The z-coordinate of sensor S15                                              |

All files in the folder `reaching_features` and `grasped_features` have the following variables:
| Name             | Type       | Unit | Description                                                                  |
|------------------|------------|------|------------------------------------------------------------------------------|
| `userID`         | `[int]`    |  --  | The user ID. Note that these are not consecutive numbers.                    |
| `object`         | `[string]` |  --  | The target object.                                                           |
| `side`           | `[string]` |  --  | The position (left or right) of the target object.                           |
| `action`         | `[string]` |  --  | The action to be performed.                                                  |
| `trialID`        | `[int]`    |  --  | The trial ID can be 0 or 1.                                                  |
| `phase`          | `[string]` |  --  | The motion phase can be `Reaching` or `Grasped`                              |
| `frameID`        | `[int]`    |  --  | The frame ID starts at 0 for each trial (s. *_raw files).                    |
| `frameTimeStamp` | `[double]` |  ms  | The frame time in milliseconds since the beginning of the trial.             |
| `vh`             | `[double]` |  m/s | Hand motion velocity (filtered with a zero-phase Butterworth filter at 15 Hz) |
| `vw`             | `[double]` |  m/s | Wrist motion velocity (filtered)                                             |
| `tia`            | `[double]` |  cm  | Thumb-Index Aperture (filtered)                                              |
| `tma`            | `[double]` |  cm  | Thumb-Middle Aperture (filtered)                                             |
| `tra`            | `[double]` |  cm  | Thumb-Ring Aperture (filtered)                                               |
| `tla`            | `[double]` |  cm  | Thumb-Little Aperture (filtered)                                             |
| `vhraw`          | `[double]` |  m/s | Unfiltered Hand motion velocity                                              |
| `vwraw`          | `[double]` |  m/s | Unfiltered Wrist motion velocity                                             |
| `tiax`           | `[double]` |  cm  | The x-coordinate of the Thumb-Index vector                                   |
| `tiay`           | `[double]` |  cm  | The y-coordinate of the Thumb-Index vector                                   |
|       ...        |     ...    |  ... | ...                                                                          |
| `tlaz`           | `[double]` |  cm  | The z-coordinate of the Thumb-Little vector                                  |

## Coordinates
We used a right-handed coordinate system with the x-axis pointing upwards, the y-axis pointing forward, and the z-axis pointing from right to left. The origin is at the *hand starting position*.

## Sensor Mapping

| Sensor | Description                                           |
|--------|-------------------------------------------------------|
| `S1`   | wrist position                                        |
| `S2`   | hand position (meta-carpal of the Middle finger)      |
| `S3`   | proximal phalanx of the Thumb                         |
| `S4`   | proximal phalanx of the Index finger                  |
| `S5`   | proximal phalanx of the Middle finger                 |
| `S6`   | proximal phalanx of the Ring finger                   |
| `S7`   | proximal phalanx of the Little finger                 |
| `S8`   | fingertip of the Thumb                                |
| `S9`   | fingertip of the Index finger                         |
| `S10`  | fingertip of the Middle finger                        |
| `S11`  | fingertip of the Ring finger                          |
| `S12`  | fingertip of the Little finger                        |
| `S12`  | *(do not use)* FT1 sensor                             |
| `S12`  | *(do not use)* FT2 sensor                             |
| `S12`  | *(do not use)* Stylus                                 |


[![DOI](https://zenodo.org/badge/955882786.svg)](https://doi.org/10.5281/zenodo.15096149)
