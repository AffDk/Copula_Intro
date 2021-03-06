## An introduction to the concept of Copula in statistical simulations

This introduction is relevant to somebody who has a fair understandig of basic stochastic processes but not really a statistician or anything like that. At the first glance the descripton found in Wikipedia does not provide much of intuition. Well, now after spending a little time to read a few blog posts and an introduction included in the documentation of Statistics and Machine Learning Toolbox of MATLAB, Wikipedia's definition makes sense too.

### it will be simpler to follow this note on the attached jupyter notebook

The story begins from the simulation of a multivariate distribution. Well, the most obvious case, would be multivariate normal distribution. To make even simpler, let us start with bivariate normal distribution. If we only have the mean and the covariance matrix, we know everything about such a distribution. Statisticians call this set (mean and covairace matrix in this case) "sufficient statistics".

We can simply generate random samples of a bivariate normal distribution with a given mean and covariance matrix.

![This is an image](/Fig1.png)

However, the problem becomes more difficult when the distribution is arbitray. Especially, the mean and covriance won't be sufficient statistics to generate the random samples following an arbitrary multivariate distribution. Here, the concept of Copula comes in handy. I assume that reader of this notebook may have come across "inversion method" to generate samples from a random variables. The point is the that cumulative distribution function (CDF) is a function which goes for the set of real numbers to an interval of [0,1]. Since a CDF is monotonic and injective (one-to-one), it is invertible. Now if we have a random generator with a uniform distribution in the interval of [0,1] and apply the inverse of the CDF to the uniformly generated samples, the result will be a random variable with a distribution characterized by the given CDF. Conversly, if a we have any random variable and calculate its CDF, the result will have a uniform distribution. It is quite simple to prove this mathematically.

Let  ????1  be a random variable with a given CDF, such that,  ????1=????????????(????1) , then:
????1???Uniform
 
Proof:

????????????????(????)=????(???????????)=????(????????????(????)???????)
 
since  ????????????<sup>???1</sup>  is ascending, it can be inserted to both side of the inequality, so we will have:

????(????????????<sup>???1</sup>(????????????(????))???????????????<sup>???1</sup>(????))=????(???????????????????<sup>???1</sup>(????))
 
this probability, dy definition, equals:
????????????(????????????<sup>???1</sup>(????))=????
 
thus,  ????????????<sub>????</sub>(????)=????  and this by defintion delineates a uniform distribution.  ??? 

This can be seen in the following figure:

![This is an image](/Fig2.png)


As proven above, the output of the  ????????????  is uniformly distributed and this can be seen in the figure above. Another interesting observation is that the rank-based correlation (e.g. Kendal  ???? ) between normally distributed random variable is preserved between the uniformly distributed variables.

Now that we have some uinformly distributed variables with certain correlation between them, if we apply the inverse of an arbitrary  ????????????  to each of the unifromly dirtributed variables, we will get a bivariate distribution whose marginals are the selected arbitray  ????????????  and we will see that they also preserve the rank-based correlation between the variates of the distribution. This constitutes the basis of the concept of Copula. It can be generalized to multivarie distributions too.

In the following example, I used the inverse of a gamma distribution and a t-distribution to simulate a bivariate distribution.

![This is an image](/Fig3.png)

Note here that the correlation is preseved in the new bivariate distribution.

Defintion of Copula
Copula is a function which satisfies certain conditions, most importantly, it represent a multivariate distribution whose martginal distributions are all uniformly distributed. Having a Copula function (C) makes the simulation of a multivariate distribution simpler. This follows Sklar's theorem which states that for an N-dimensional distribution with continuous margins  ????1,????2,...,???????? , there exist a Copula function for which:

????(????1,????2,...,????????)=????(????1(????1),????2(????2),...,????????(????????))
 
Note here  ????(????????)  is a comulative distribution function and will have a uniform distribution. Similar to the relationship between cumulative distribution function and probability distribution function where  ????(????)=????????/???????? , partial derivative of Copula function is defined as below:

????(????1,????2,...,????????)=???????(????1,????2,...,????????)/???????1???????2...???????3
 
then, the probability distribution function of the multivariate distribution will be:
????(????1,????2,...,????????)=????(????1(????1),????2(????2),...,????????(????????))???????=1????????????(????????)

Now imagine we have some realizations of two random variables that I call them original random variables and we'd like to simulate a bivariate distribution whose marginals follow a distribution corresponding to the original random variables with certain correlation.

![This is an image](/Fig4.png)

Obviously, there are a lot more about the concept of Copulas and how to simulate various forms of correlation structure. For example, the correlations which varies for extreme values and here I only mentioned a few things about what is known as elliptical Copulas. Anyhow, this notebook has used several other tutorials to put together a hopefully concise basic introduction to this concept.
