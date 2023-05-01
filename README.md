# Control and Trajectory Tracking for Autonomous Vehicle
## The Code and The Results
In this project, a PID controller is designed in order to perform vehicle trajectory tracking. Given a trajectory as an array of locations, a PID controller controls an ego vehicle and its efficiency is tested on the CARLA simulator used in the industry.

Installation

Run the following commands to install the starter code in the Udacity Workspace:

Clone the [repository](https://github.com/udacity/nd013-c6-control-starter.git):

```zsh
git clone https://github.com/udacity/nd013-c6-control-starter/tree/master
```
## Run Carla Simulator

* Write in new Terminal

```zsh
su - student
// Will say permission denied, ignore and continue
cd /opt/carla-simulator/
SDL_VIDEODRIVER=offscreen ./CarlaUE4.sh -opengl
```

## Compile and Run the Controller

* Write in new Terminal

```zsh
cd ./project
sh base_setting.sh ## This command will execute everything that is needed to be set from "./install-ubuntu.sh" to "cmake ." and "make"
```

## Testing

* To test your installation run the following commands.

```zsh
cd ./project
./run_main_pid.sh  //This will silently fail ctrl + C to stop
./run_main_pid.sh  //(again) Go to desktop mode to see CARLA
```
* If error bind is already in use, or address already being used
```zsh
ps -aux | grep carla
kill id
```

## Project Instructions

In the previous project, a path planner for the autonomous vehicle has been built. Now a steer and throttle controller is built so that the car follows the trajectory.

In the directory ./project/pid_controller you will find the files pid_controller.cpp and pid_controller.h. This is where you will code your pid controller. The function pid is called in main.cpp.

## Step 1: Build the PID controller object

Complete the TODO in the pid_controller.h and pid_controller.cpp.

Run the simulator and see in the desktop mode the car in the CARLA simulator. Take a screenshot and add it to your report. The car should not move in the simulation. To find this result shown in image below and the car not moving

<img src="/Project/Images/Control.png">

## Step 2: PID controller for throttle and steer:
In main.cpp The code Commented and I Tuned the parameters of the pid as possible.

Find the result video in folder images with some other videos for tunning trials in folder bad and trio crash

## Step 3: Evaluate the PID efficiency

The car performed well along the road after many trials at PID parameters as follows:
Throttle Kp (proportional gain): 0.2
Throttle Ki (Integral gain): 0.0005
Throttle Kd (Derivative gain): 0.0005
Note the initialized values I have started at are (kp = 0.1, ki = 0.0001, kd = 1.0) which
are recommended by project guide.

<img src="/Project/Images/Steering Error.png">

<img src="/Project/Images/Throttle.png">

Based on the plots, how does each part of the PID affect the control command?

The proportional gain (Kp) amplifies the error signal and dictates how much the controller reacts to the current error. A high Kp value leads to a more aggressive response by the controller to the error, but it may also cause instability and overshooting.

The integral gain (Ki) responds to the accumulated error over time and aims to eliminate the steady-state error signal. A higher Ki value causes the controller to react more strongly to long-term errors, but it may also result in oscillations and instability.

The derivative gain (Kd) responds to the rate of change of the error by introducing a term that is proportional to the derivative of the error signal, reducing overshoot and oscillation. However, a high Kd value causes the controller to respond more aggressively to sudden changes in the error, which may also lead to instability and overshooting.

## How would you design a way to automatically tune the PID parameters?

By implementing Twiddle, as taught in the lessons, the code will iterate through and test various PID parameters to find the optimal combination that produces the least error.

## PID controller is a model free controller, i.e. it does not use a model of the car. Could you explain the pros and cons of this type of controller?

Advantages: It is simple to comprehend and can be implemented in a wide range of systems without requiring a system model.

Disadvantages: It can be challenging to fine-tune and may not be as precise as other controllers that rely on the system model.

## What would you do to improve the PID controller?

By utilizing Twiddle or the Ziegler-Nichols method, the PID parameters can be fine-tuned to achieve better results. Since I am using a simulation, it should be feasible to implement either of these methods.
