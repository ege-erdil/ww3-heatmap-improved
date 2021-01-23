# ww3-heatmap-improved
Inferring a probability distribution over the world map about possible WW3 breakout incident locations from Metaculus question data using Gaussian cluster analysis

This Python script infers a joint probability distribution over the world map from the two marginal distributions over latitude and longitude given at https://www.metaculus.com/questions/3867/if-there-is-a-ww3-what-longitude-will-it-start-in/ and https://www.metaculus.com/questions/3868/if-there-is-a-ww3-what-latitude-will-it-start-in/ for the location of the incident that will lead to WW3, conditional on WW3 indeed happening before end of year 2049. To do this, I assume that the true probability distribution comes from independent contributions of a number of high risk areas which are spatially localized, suggesting that a convex combination of a small number of Gaussian modes (with covariance matrices restricted to be some multiple of the identity) can give a good fit to the two marginal distributions given in the questions.

The Powell optimizer in the scipy library works quite fast for a number of modes up to around 5, after which it becomes quite slow, but the fit is already quite good even with only 3 modes: the sum of the Kullback-Leibler divergences of the marginal distributions obtained from the model and the actual marginals from the community forecasts gets somewhere below 0.1 nats, which is quite a good fit. There's also significant sensitivity to initialization in the optimizer. I might switch to a gradient-based optimizer if I ever get around to writing a Jacobian for the objective loss function, which is the mentioned sum of two Kullback-Leibler divergences; one with the latitude distribution and the other with the longitude distribution.

The script also produces a heatmap over a world map using pyplot for visualization purposes.
