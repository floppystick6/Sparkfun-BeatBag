# Sparkfun-BeatBag
Crowdsourcing an algorithm 

For more info see https://www.sparkfun.com/news/2115

AlgorithmOnly - is the code needed to implement the algorithm

Code+Algorithm - is Nate's original code with the algorithm added in


--------------------
This is my algorithm:

1) Read the accelerometer and get a 3 dimensional vector, call it curV. 

2) Subtract the previous vector (prevV) from curV. This results in the difference vector, aka the delta vector (∆V)

3) Given the time stamps for the vector readings, we can find ∆t = (curV time stamp) - (prevV time stamp).

4) Find the Magnitude of ∆V (Mag∆V) to see how much the curV changed from the prevV.

5) Divide Mag∆V by ∆t to find the rate of change in the acceleration. This is the Jerk (https://en.wikipedia.org/wiki/Jerk_(physics))

6) Then check this Jerk against a minimum threshold to filter out jerks caused by incidental "accelerations". 

  - Based on the raw data provided, I found 650 to be a good Jerk minimum threshold. 
  - 
7) If the Jerk is greater than the minimum threshold, then check and make sure that the Jerk occurred x amount of time after the last
one. 
  - This is to filter out the bag bouncing back and forth after a single hit. 
  - 
  - Based on the raw data provided, I found 60ms to be a good minimum time between Jerks. 
  - 
8) If the Jerk passes both of these tests, then we can consider it a HIT. 
