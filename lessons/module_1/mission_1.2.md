---
index: 3
module: module_1
task: test_drive
previous: sandbox
next: python_variables_commands
---

# Mission 1.2 Test drive

## Objective

Understand the concept of a "Robot Object" and execute your first movement code.

![Beginner](https://img.shields.io/badge/Difficulty-Beginner-green)

## Introduction

In this lesson, you will initiate the robot's movement. But before we push the button, we need to understand *who* receives our commands.

Behold the mighty rover who will assist you in learning:

![Picture of the robot](https://github.com/autolab-fi/Metropolia-Line-Robot-Course-2ECTS/blob/main/images/module-1/robot.jpg?raw=true)


## Theory: The Digital Twin

Computers don't know what a "rover" is until we tell them. In Python, we create a specific software representation of our hardware.

Look at this line of code:
```python
robot = Robot()
```

Here is what happens:
1. **`Robot()`** refers to the **Class** (the blueprint or instructions on how to build a robot).
2. **`robot`** is the **Object** (the specific robot we just created).

Think of it this way: `Robot()` is the factory, and `robot` is the specific machine that rolled off the assembly line. We will send all our commands to this `robot`.

## Assignment

You will run exactly the same program twice: first in the simulator and then on
the physical robot.

1. Copy the code below into the code editor.

```python
from lineRobot import Robot

robot = Robot()

robot.move_forward_seconds(3)
```

2. Run the program in the simulator and make sure the simulated robot moves
   forward for three seconds and stops.
3. Keep the code unchanged and submit it to the physical robot.
4. Watch the physical run in the video feed and wait for the automatic result.

The assignment is checked automatically. There are no quiz questions or written
answers.

## Conclusion

You have now executed the same Python program in a digital twin and on real
hardware. You can proceed to the next lesson.
