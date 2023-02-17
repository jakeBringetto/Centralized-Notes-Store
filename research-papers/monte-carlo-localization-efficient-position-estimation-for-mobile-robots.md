# Monte Carlo Localization: Efficient Position Estimation for Mobile Robots

[http://robots.stanford.edu/papers/fox.aaai99.pdf](http://robots.stanford.edu/papers/fox.aaai99.pdf)

### Summary

The motivation for this paper is to do localization in a novel way. Previously, localization methods have been very effective, yet they are computationally expensive. This paper presents a version of markov localization based on sampling that is computationally efficient while also keeping the ability to be effective at localization.

The problem at hand is to track the position of robots where there is a small degree of uncertainty regarding it's true position. Other methods that have been explored such as kalman filters and grid based approaches have proven to be computationally burdensome at this task. Monte Carlo Localization counters this by using fast sampling techniques to estimate the posterior distribution representing the estimated position of the robot.  This method is more efficient, very accurate, uses less memory, and is very easy to implement.

Delving more into the details of the approach, Monte Carlo Localization is a version of Markov Localization, which works by creating a probability distribution modeling posterior probability. It uses bayes rule and known information about the robots prior probabilities and observations in real time to create the posterior. The two phases of MCL are robot motion and sensor reading. When the robot moves, the authors of the paper generate N samples of the estimated position using a precomputed sample set. Then, the robot uses the sensor reading to update the posterior probabilities using bayes rule.

In addition to to the above, MCL has adaptive sample size, where the size of the sample set is adjusted based on what is needed to obtain a certain accuracy.  This is done using variance of the estimated positions before and after sensor readings. Based on whether this divergence is high or low, they adjust the sample set size accordingly.

Overall the results of this sampling based method were very effective. Compared to other markov localization approaches such as kalman filters and grid based approaches MCL was much more computationally effecient and used less memory. Additionally, even when using adaptive sample sizes, the accuracy was still very high.

