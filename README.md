# Sunspot Analysis

## Requirements and Background

The data used here comes from the Sunspot Index and Long Term Solar Observations. The following packages were used in order to complete the analysis and subsequent forecasting:

- Plotly <br>
- Pandas <br>
- Statsmodel <br>
- Numpy <br>
- Scipy <br>

This project is part of my portfolio in order to display how to perform exploratory analysis on data that i found interesting. Below you will find the steps that I took and the plots that were generated. The data used can be found here: https://www.sidc.be/silso/datafiles.

## The Solar Cycle

The sun's solar cycle is about 11 years long and this can be measured using the number of sunspots that are visible to us. For the past 200+ years humans have been able to record this and track this cycle. 

## Exploratory Analysis

The first steps was completing an exploratory analysis on the dataset. The below plots were generated for this: <br>

![image](https://user-images.githubusercontent.com/95090904/219228284-fb869885-f12e-45d2-9ad2-8ad0e84a044a.png)

![image](https://user-images.githubusercontent.com/95090904/219228362-45232bb4-aaef-4bd4-9b43-bf5dac65f527.png)

![image](https://user-images.githubusercontent.com/95090904/219228423-989d636a-5fec-4a8c-948d-f46742093b8c.png)

![image](https://user-images.githubusercontent.com/95090904/219228462-7906e31a-9710-4919-b8f0-1a4099b1dd3b.png)

From the above plots we can see that the maximum average and actual maxiumum occured in the 1820's and has been decreasing since that point. We can also see that in the below plot on the overall time series.

![SunSpot_timeSeries](https://user-images.githubusercontent.com/95090904/219223978-b8318058-8264-4b96-9cc5-323f8d2f29cb.png)

We can also overlay the different sun cycles in order to compare them better.

![sunspot_overlay](https://user-images.githubusercontent.com/95090904/219224208-cec0054d-3ad9-4fa1-abb0-43faa0145972.png)

We can clearly see that some years are much more active than others. 

# Creating a Simple AR Model

Using the lags from the partial autocorrelation chart we can see that the 1st, 2nd, 3rd, 4th and possibly the 8th and 9th are correlated to the first lag. Therefore we can chose a function that looks something like this:

```math
\begin{align} f(x) = {\beta_0} + {\beta_1*x_{t-1}} + {\beta_2*x_{t-2}} + {\beta_3*x_{t-3}} + {\beta_4*x_{t-4}} + {ϵ} \end{align}
```

We are going to start with the 4 lags that are possibly correlated and if we need to add more we can. Once the model is run we can get an idea of how it is going to perform by looking at the residuals.

![image](https://user-images.githubusercontent.com/95090904/219230501-51e6f6ee-5379-459a-a24e-053028252e79.png)

The plot shows that there is something that we are most likely missing the data and not capturing in the model. We can also clearly see that from the stats below:

Mean Absolute Percent Error: 3.605 <br>
Root Mean Squared Error: 47.4090714934382

There are several steps that we could take in order to improve the model potentially. The are as follows:

- Reduce the amount of lags to 3 because we know that the 4th is not significant
- Add additional lags based on the partial autocorrelation plot
- Reduce the time period we are going to predict due to the fact that as we get further out in predictions the accuracy will go down.

The above options would be our next steps in order to try and improve the accuracy of the model. 
