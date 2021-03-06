# Probability Distributions and Random Variables

**Quick question is why do we need to talk about probability distributions. What does it have to do with data?**

<div style="text-align: justify;">
It is like a mathematical concept, if we look at the use of the histogram we express that as a way of describing data.</div>

![alt text]( https://raw.githubusercontent.com/AbhishekKumar4/Data-Analytics/master/Probability%20Distributions%20and%20Random%20Variables/Probability%20Distributions%20and%20Random%20Variables%20Intro/distri.png)
<p style='text-align: justify;'>If we look at this picture above, the histogram is those vertical gray, grayish blue bars that you see on this graph and that describes the data that summarizes the data in some way. But if we collect a new sample we will get bars that looks slightly different and the question is, is it really coming from a probability distribution, is it coming from some other mathematical function that closely approximates this histogram that you are seeing. And that red line that you see on this is the attempt to fit this mathematical function.</p>

<p style='text-align: justify;'>The core idea here is this data is being generated by this probability distribution function, which is that red line and the histogram is, what we see in terms of data. Because, not every time we going to get data that looks exactly like the red line, so it is in this context that we can think of a probability distribution also as a way of just describing our data. But, we would say describing and not summarizing, because it is fairly comprehensive, it just does not give us one number or one thing. It gives the full form and shape of that data and we can think of it as an exercise also in modeling our data.</p>

<p style='text-align: justify;'>So, we are not just describing it, you modeling it. So, in that context probability distributions are very important and we will also see how in various other things, not just describing data, but even in terms of doing more advanced analytics in the machine learning parts in the statistical inference parts, the use of probability distributions is critical.</p>

<p style='text-align: justify;'>Think of a data set that has random numbers that are being generated in accordance to some mathematical function is the whole idea behind, the use of probability distributions with respect to data.</p>


# Random variables
Variable whose value is subject to variations due to randomness.The distinguishing factor between a variable and a random variable is that, with a regular variable once you fix all the externalities, then the variable takes on a specific value.

For example : F = m * a

Force can be any possible value, it can take on various numbers as it is value with some units. But, once you fix mass and you fix acceleration, force will take on a very specific value. **As oppose to a random variable**

and **The mathematical function describing this randomness is called probability distribution.**


**We can broadly break up the idea of probability distributions into discrete probability distributions in continuous distributions.**

 # Discrete probability distributions
Which is that the probability something happens is x. So, we might say the probability that rains today is 10 percent, What goes unsaid is that, there is therefore, a 90 percent chance that it does not rain today. Essentially we are talking about these kind of binary events, where one of the possible outcomes is x and therefore, by definition the remaining possible is just 1 minus x or if we are thinking of it in terms of percentage, then its 100 minus x.

- Another very simple example of this could also be something like there is a 50 percent chance that, if we toss the coin we are going to get heads and what goes without saying is therefore, that there is a 50 percent chance that we would not get heads. In this case, that is called tails. So, that is one very simple conception of probability and this is a probability distribution, it is called **Bernoulli distribution** (To be discussed later), but we can move to multiple outcomes.

-  If we role a dice. we either get 1 or 2 or 3 or 4 or 5 or 6 and the idea is that the probability of each of these is one sixth, if it is a fair dice and so, that is a different kind of a probability distribution. That is called **discrete uniformed distribution** (To be discussed later).If we take all the possible values and take each probability and you add them all, we always get 1. we have comprehensively covered the universe of possibilities,
**This is why, the probability distributions sum to 1**

-  Assume that, we have this coin and we want to describe this random variable, which is the probability of getting a heads or a tails and that is the random variable and we do not want to assume anything , there is a 50, 50 chance. So we do a data collection exercise, where we toss the coin 30 times and notice that we get 14 heads and 16 tails and for whatever reason, if we do not want to assume anything about the distribution and let us say. So, we are going to actually say 14 by 30 is the probability of getting a heads and 16 by 30 is the probability of getting a tails. Here we just wanted to take data and wanted to describe a probability distribution with the data, then we can definitely define a discrete distribution in this way.

# Continuous Distributions
This is the same core concept of describing the distribution, but here the x axis is not discrete.
For example probability of a certain height. A height can be a 180 centimeters, so that could be one number out here, but it could also be 150.001 centimeters, it could also be a 129.999 centimeters. We cannot possibly roll the dice and get a 2.5, whereas in measure of height we could get any possible value within the certain range.

-Important thing to note is just like in the discrete distributions, where we said the sum of all the probabilities for each possibility should add up to a 100 percent or should add up to 1. Here we cannot have a countable number of possibilities, so we cannot take each possibility. Take the probability of that and added to 1, just because there are infinite number of them. So, basically what we do is, we take the entire interval and sum the probability within that interval and the best way to do that is to look at the area under the curve as a whole. So, this way when we look at this area, it is like we are taking all the possibilities within that area and summing all the probabilities for each possibility and when we do that, we will be getting 1 or a 100 percent.

# CDF (cumulative density functions) and PDF (probability density functions)

- For each probability density function, there exist a cumulative density function.

**we will discuss it in the continuous case and that is the easiest and then separately do that for the discrete.**

**PDF**
Because there are infinite number of possible states, it does not really make sense to ask the question, what is the probability at a given point.

It turns out that the answer to that question is that the probability of that given point is zero, although there is some y, there is some height for that given point. Because, there are infinite such points out here, because there are technically infinite such points. As a result, we can get the probability of given area by just measuring the area under this curve.

**CDF**
Describes the cumulative probability up to a certain point.
The cumulative describes the probability from zero, from the lower end of the axis and that can be zero or that could be something like minus infinity or it could be some other value. From the starting point to all the way up to the point of interest.

**way of getting from a PDF to CDF and from CDF to PDF

PDF to CDF - Integrate ( Integrate up to a point x, so let us say just that this started at zero, but we could change
that.)

CDF to PDF - Differentiate ( Differentiate the CDF and that will give us the PDF).
