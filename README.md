# The Simplest Explanation about PID (NGL!) 😎✨
## Chapter 1: Introduction to Control Engineering 🔧🛠️

$$
u(t) = K_p e(t) + K_i \int_0^t e(\tau) d\tau + K_d \frac{d}{dt}e(t)
$$

That's the well-known PID formula. It looks hairy, doesn’t it? As the name stands for <b>P</b>roportional, <b>I</b>ntegral, and <b>D</b>erivative. Why bother with the whole package of calculus to control such a system?

Well, first of all, we have to dig down to understand why we needed a controller in the first place. A naked system could still be functional, but if we talk about automation, a tiny error could lead to a huge problem. This is why we need control engineering. Hold on, what's the actual job of control engineering? 🤔

The job of control engineering is to make sure the input signal produces the desired value as the actuators' movement. Sometimes there might be external factors such as changes in load, temperature, electrical noise, etc. This could lead to deviations in the actuator’s behavior if we simply use the voltage value as an input. This is why control engineering comes in handy. 💡

## Chapter 2: Introduction to PID Controller 🔍

As we mentioned in Chapter One, the PID controller has three components: P, I, and D. The main idea about PID is to use feedback to calculate the value between the current point and the desired point (error). What happens when the error is known? 🧐

Well, imagine you're on a quest to find a hidden treasure. You have a map that shows the location of the treasure (the desired point or setpoint), but you don’t know exactly where you are in relation to it. As you explore, you receive clues (<i>feedback</i>) that tell you how far you are from the treasure (this is the error or the difference between your current location and the treasure's location). Once you know the error, you can make decisions about how to adjust your course to get closer to the treasure. 🗺️💎 When you first realize how far away you are from the treasure, your instinct is to take a step forward toward the treasure accordingly. If your current position is really far away from the treasure, you might want to run to get there as quickly as possible. Although if your current position is really close to the treasure, you might want to slow down and look around carefully. 🏃‍♂️🚶‍♀️

## Chapter 3: The Effect of the Proportional (P) Variable 📏

You want to go to your friend’s house. Let's say it's 100 meters apart from your current location. The controller would take the difference value between the current state and the desired state (which is 100 meters), then multiply the value by the <b>P</b> constant value or <b>P</b> gain. Another thing to remember, PID uses feedback. So, somehow you have a tracker device to measure how far apart you are from your friend's house. 🏠

$$
u(t) = K_p e(t)
$$

$K_p$ is the <b>P</b> gain, which you can change (this variable is customizable). $e(t)$ is the error as a function of time. Can you imagine what will happen based on the formula? Since at the beginning the value of $e(t)$ is high, $u(t)$ will likely be a high number. Gradually, as you move closer to your friend’s house, $e(t)$ will decrease. That will result in a change in $u(t)$ proportional to the change in $e(t)$. At some point, the value of $e(t)$ will be zero, which means you're at your friend's house. Since $e(t)$ is zero, the system will stop because $u(t)$ will also be zero. 🎯

## Chapter 4: The Effect of the Integral (I) Variable 🔄

Why do we need another variable to think of? Isn’t **P** good enough? Well, it is not always the case. Sometimes more sophisticated systems need more complex tools. 🤯

Let's say when you went to your friend's house, your friend wanted to make an autonomous quadcopter drone that hovers at 50 meters. Therefore, you wanted to help your friend's project by composing the algorithm for it. 🚁

When you start flying, your drone is not at 50 meters yet. The error, $e(t)$, is the difference between the current height and 50 meters. So, the control output, $u(t)$, is high because the error is large. This helps the drone to ascend quickly. 

As the drone gets closer to 50 meters, $e(t)$ decreases. This means $u(t)$ decreases too. When the drone reaches 50 meters, $e(t)$ becomes zero, and $u(t)$ also drops to zero. Zero control value mean there's no value being input into actuator. This could lead to the drone stopping to running and drop down. 📉 Therefore, after a few second the feedback will notify the system that there's a difference between desired value of height with the actual value or $e(t)$ isn't zero, that'll resulting in $u(t)$'s value, and the cycle will go on and on. This might lead to the drone rising again and dropping back down, creating oscillations. 🛫🔄

Now, let’s see why we need a Proportional-Integral (PI) controller:
- **Prevent Oscillations**: The PI controller adds an Integral (I) component to the mix. Imagine the Integral action as a gentle reminder that keeps track of all the small errors over time. If the drone drifts slightly below 50 meters, the Integral action starts to accumulate this error. Over time, this accumulated error will influence $u(t)$ to correct the drift and stabilize the hover. 🕒🛠️
- **Eliminate Steady State Error**: Let's make a little abstraction. We don't know the drone yet, but for the purpose of example, the motor's drone needed exactly 100 RPM for the drone to hover. Therefore we have to make the output equal 100 RPM to make the drone hover. Here's a little problem if we use a P controller:
  - *error x **p** gain = motor speed*
  - *50 m x 2 = 100 RPM*
  - *20 m x 5 = 100 RPM*
  - *10 m x 10 = 100 RPM*
  - *1 m x 100 = 100 RPM*

  Somehow, to maintain at 100 RPM the error will still exist. This is called **steady-state error**, the persistent difference between the desired value and the actual value. Imagine the **I** variable as a memory that remembers all the small errors over time. If the drone has consistently not reaching the target speed, this memory accumulates this error. Over time, this accumulated error leads to a gradual adjustment to correct the persistent shortfall. ⚙️📉

 If you only use Proportional control, you adjust based on current error. But if there’s a tiny, constant error, the Proportional controller might not fix it completely because it only responds to the present error, not the historical or past error. This means you’ll still have a small, ongoing difference between the desired and actual speeds.
 
 The Integral part of the PI controller keeps track of the total accumulated error over time. If there’s a steady, small error, the Integral action gradually increases its correction to eliminate this error. It makes sure that even the smallest, persistent difference is adjusted so that the drone reaches and stays at the exact desired speed or height.
 
$$
u(t) = K_p e(t) + K_i \int_0^t e(\tau) d\tau
$$

## Chapter 5: The Effect of the Derivative (D) Variable 🧮

## Chapter 6: Implementing PID in Omniwheel System 🚀

## Chapter 7: Code Walkthrough and Explanation 💻

## Resources 📚
