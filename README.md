# Extended Kalman Filters

---

**Extended Kalman Filters Project**

The goals / steps of this project are the following:

* Setting up the appropriate matrices for the lidar and radar sensors
* Implement a Kalman filter algorithm that first predicts the object position and then updates the prediction using the new measurement
* The RMSE (root-mean-square error) of the position data px, py, vx, vy should be less than or equal to the values [.11, .11, 0.52, 0.52]

[//]: # (References)
[simulator]: https://github.com/udacity/self-driving-car-sim/releases
[win 10 update]: https://support.microsoft.com/de-de/help/4028685/windows-get-the-windows-10-creators-update
[uWebSocketIO]: https://github.com/uWebSockets/uWebSockets
[linux on win 10]: https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/
[MinGW]: http://www.mingw.org/
[CMake]: https://cmake.org/install/

---

## Files Submitted & Code Quality

### 1. Submission includes all required files and every TODO task has been accomplished 

For this project I have modified the following five files:
```cpp
FusionEKF.cpp
FusionEKF.h
kalman_filter.cpp
kalman_filter.h
tools.cpp
```

The ```FusionEKF.cpp``` files initializes all process and measurement matrices from line 37 - 67. After the first initialization of the state `ekf_.x_`, the state then gets predicted in the `void KalmanFilter::Predict()` function on line 20 in the ```kalman_filter.cpp``` file. After the prediction we update the state and covariance matrices based on the sensor type from line 153 - 163 in ```FusionEKF.cpp```. The `void KalmanFilter::UpdateEKF()` function on line 30 in the ```kalman_filter.cpp``` file updates the measurement. Here we distinguish between the standard and the extended Kalman filter based on the sensor type.
The `VectorXd Tools::CalculateRMSE()` function on line 12 in the ```tools.cpp``` file calculates the root-mean-squared error and returns the value. 

### 2. Code must compile without errors

This project was done on Windows 10. In order to set up this project I had to:
* update my Windows 10 Version with the [Windows 10 Creators Update][win 10 update]
* install the [Linux Bash Shell][linux on win 10] (with Ubuntu 16.04) for Windows 10
* set up and install [uWebSocketIO][uWebSocketIO] through the Linux Bash Shell for Windows 10
* [download the simulator from Udacity][simulator]

**To update the Linux Bash Shell to Ubuntu 16.04 the Windows 10 Creators Update has to be installed!**

Also [CMake][CMake] and a gcc/g++ compiler like [MinGW][MinGW] is required in order to compile and build the project.

Once the install for uWebSocketIO is complete, the main program can be built and run by doing the following from the project top directory in the Linux Bash Shell.

1. `mkdir build`
2. `cd build`
3. `cmake .. -G "Unix Makefiles" && make` on Windows 10 or `cmake .. && make` on Linux or Mac
4. `./ExtendedKF`

Then the simulator has to be started and *Project 1/2: EKF and UKF* has to be selected. When everything is set up the Linux Bash Shell should print: 
```bash 
Listening to Port 4567
Connected
```

---

## Discussion

### 1. Briefly discuss any problems / issues you faced in your implementation of this project.
My program crashed several times when I clicked the "start" button. The stacktrace was: `ExtendedKF: [...] Assertion 'index > = 0 & & index < size()' failed. Aborted (core dumped)`. This happens if a vector and/or matrix has not been initialized anywhere in the code.
So I had to debug my code by printing out statements in the Linux Bash Shell with ``std::cout`` to narrow down which vector or matrix has not been initialized. After I have found the error the program was running as expected.
