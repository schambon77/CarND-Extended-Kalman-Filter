# Extended Kalman Filter Project
Self-Driving Car Engineer Nanodegree Program

## Project Objectives

In this project, a kalman filter is utilized to estimate the state of a moving object of interest with noisy lidar and radar measurements. The goal is to obtain RMSE values lower than the tolerance outlined in the project rubric.

## Project Files

* [Source code](https://github.com/schambon77/CarND-Extended-Kalman-Filter/tree/master/src)
* [ReadMe](https://github.com/schambon77/CarND-Extended-Kalman-Filter/blob/master/README.md)

## Project Rubric Points

The project rubric points can be found [here](https://github.com/udacity/CarND-Extended-Kalman-Filter-Project).

### Compiling

The [source code](https://github.com/schambon77/CarND-Extended-Kalman-Filter/tree/master/src) compiles without errors with `cmake` and `make` by executing the following commands from the repository top folder:
1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./ExtendedKF

### Accuracy

When testing with data set 1 in the simulator, the px, py, vx, vy output coordinates have an RMSE that meets the success criteria of <= [.11, .11, 0.52, 0.52].

### Follows the Correct Algorithm

The Sensor Fusion algorithm follows the general processing flow as taught in the preceding lessons.

The `FusionEKF` constructor finishes the initialization of the matrices `F`, `Q` and `H_laser`, as well as the process noise constants. 

The`FusionEKF::ProcessMeasurement()` method handles the first measurements appropriately, whether it is a laser or radar measurements, in order to initialize the state vector `x` and covariance matrice `P`.

The Kalman Filter algorithm carries on to first predict, then update.

Upon receiving a measurement after the first, the algorithm predicts object position to the current timestamp by using the tie difference with the previous timestamp.

The algorithm then updates the prediction using the new measurement. It can handle both radar and lidar measurements. The algorithm does so by setting up the appropriate matrices given the type of measurement, in particular the Jacobian Hj matrix in the case of radar sensor measurements. It then calls the correct measurement function for the given sensor type (`kalman_filter::Update()` for laser measurements, `kalman_filter::UpdateEKF()` for radar measurements). The `UpdateEKF()` also shows the particularity to apply the `h` function to state vector `x` to predict `z`, in order to convert cartesian to polar coordinates.

### Code Efficiency

The algorithm tries to avoid unnecessary calculations.
The prescribed [code style](https://google.github.io/styleguide/cppguide.html) is respected as much as possible.
The source code was edited with the Eclipse IDE for C/C++ Developers (Oxygen).
