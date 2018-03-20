# PID-Controller
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid` or `./pid Kp Ki Kd`. Kp Ki and Kd are parameters you want to tune with, and they are unsigned double type. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Project Instructions and Rubric

Here is a conclusion of advantages and disadvantages of three terms of PID controller in the terms of stability, fast transient response, steady-state error and overshoot.

1. Proportional Control:
- Stability: excessively large values of Kp cause instability
- Fast transient response: large values of Kp speed up the response 
- Steady-state error: non-zero steady-state errors can result
- Small overshoot: large values of Kp will cause overshoot

2. Integral control
- Stability: integral control helps stability
- Fast transient response: the transient has to be compensated for with time-consuming overshoot
- Steady-state error: integral control drives the steady-state error to zero
- Small overshoot: any negative error in the transient has to be compensated for with
overshoot

3. Differential control
- Stability: excessively large values of Kd amplify noise and cause instability
- Fast transient response: differential control slows down the transient response
- steady-state error: non-zero steady-state errors can result
- Small overshoot: large values of Kd decrease overshoot

The code could build and run sucessfully. PID contoller has followed the standard process.

The program supports inputting arguments from command line, following  `./pid Kp Ki Kd` which enables I tune the parameters easily. I have tried several combinations with/without each part and tune the values up and down like:

- `./pid 1.5 0.0 0.0`
- `./pid 0.0 0.1 0.0`
- `./pid 0.0 0.0 2.0`
- `./pid 1.5 0.1 0.0`
- `./pid 1.5 0.0 2.0`
- `./pid 0.0 0.1 2.0`

PD contoller with Ki performed well actually, but has a intergral part controls the error in reality, so I choosed a full PID contoller with parameters:
  - `Kp = 0.02, Ki = 0.001, Kd = 3.0`

  It's also the default parameters without arguements input in the command line.

  The result looks smooth and it could finish laps and laps well in simulator. 
