# CarND-Controls-PID
Reflections on Project 5 Term2.



## The Model

The model that has been used is global kinematic model.
The following set of variables are called state x,y,psi,v,cte,epsi and all the symbols for these state variables are as inteneded in the class.
The actuation controls are delta and a where delta is used for controlling steering angle and a for acceleration.
The following are the equations of global kinematic model
 1. x_[t+1] = x[t] + v[t] * cos(psi[t]) * dt
 2. y_[t+1] = y[t] + v[t] * sin(psi[t]) * dt
 3. psi_[t+1] = psi[t] + v[t] / Lf * delta[t] * dt
 4. v_[t+1] = v[t] + a[t] * dt
 5. cte[t+1] = f(x[t]) - y[t] + v[t] * sin(epsi[t]) * dt
 6. epsi[t+1] = psi[t] - psides[t] + v[t] * delta[t] / Lf * dt

The Lf in the equation is the length from front to Center of Gravity of the vehicle.


## Timestep Length and Elapsed Duration
   
   Number of time steps chosen was 25 and elapsed Duration was set to 0.05. This was tried by default as per the assignment. Later during the project the value of N was increased and decreased in the range of 10 to 28 was accomodated for a smooth ride values between 15 and 25 was found to be reasonable and values between 0.03 and 0.08 were tried and 15 and 0.05 were finally choosen to be good enough with a speed of around 25-30mph


## Polynomial Fitting and MPC Preprocessing

   Waypoints were computed by converting the coordinate values from local co-ordinate system to global co-ordinate system and then polynomial fitting was done using the polyfit function provided in the class as well as part of source code in the project. 



## Model Predictive Control with Latency
   The MPC was accomodate for the latency in actuation by choosing the values of prediction which accomodates for Latency. For example in this project Latency was chosen to be 100 milliseconds and the predictions were done at every 0.05 seconds so a computation for index which would be chosen out of the set of values predicted will be 100/50=2. So the second predicted value among the series of values, arranged according to the time steps, is chosen as the set of actuations
