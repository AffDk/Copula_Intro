## An introduction to the concept of Copula in statistical simulations

This introduction is relevant to somebody who has a fair understandig of basic stochastic processes but not really a statistician or anything like that. At the first glance the descripton found in Wikipedia does not provide much of intuition. Well, now after spending a little time to read a few blog posts and an introduction included in the documentation of Statistics and Machine Learning Toolbox of MATLAB, Wikipedia's definition makes sense too.

The story begins from the simulation of a multivariate distribution. Well, the most obvious case, would be multivariate normal distribution. To make even simpler, let us start with bivariate normal distribution. If we only have the mean and the covariance matrix, we know everything about such a distribution. Statisticians call this set (mean and covairace matrix in this case) "sufficient statistics".

We can simply generate random samples of a bivariate distribution with a given mean and covariance matrix.

