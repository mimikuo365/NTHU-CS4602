# Assignemnt 1 - COVID-19 Forecast

## **Models and Features**

I used auto regression models with the number of cases in previous days as features.

## Getting Started

### Packages Used

- tqdm
- pandas
- statsmodels>=0.12
- sklearn
- numpy
- scipy

### Install Requriements

    pip install -r requirements.txt

### Train Models and Forecast

To generate the result of the prediction, one can run through 107062374_model.ipynb cell by cell.

## Methodoogy

### Pre-processing

1. Cases with nagaive numbers <br>
    
Some of the numbers of cases in the csv downloaded from the website are negative, which are not reasonable. Two measures are proposed to fix this problems. One is setting all negative value to 0, and the other is applying absolute function (np.abs()) to negative value

In this project, I applied the second measure to the dataset, since, by observation, the second value seems more likely to the original data.

2. Cropping data

    Most of the data in the early phase of the COVID-19 outbreak are not accuracy, due to the low awareness of the disease. Therefore, in this project, I trained the model only with the data later than 1st July 2020.

3. Smoothing

    There are some noise in the raw data. To smooth the curve of number of cases, I applied a Savitzky-Golay filter with window size 51 (days) and polynomial order of 3.

### Model

1. Auto Regression (AutoReg)

    The atuo regression model is build with a python package statsmodels. The primary tunable parameter is the window size for auto regression.
In this project, the window size for auto regression is different from model to model; that is, different countries have different window size for auto regression. The range for the window size is [5, 51].

2. ReLU

    As mentioned above, the cases should not be negative, but this is not always the case for auto regression. Therefore, I wrote a ReLU (Rectified Linear Unit) function, which would set negative values to zero, and apply it to the output of auto regression prediction.

3. Round to Int (rint)

    Number of cases should not be fractional. I rounded them to integers before produce the final prediction.

## Performance

Below are the plots of ground truth data and prediction in the test data for five countries - Russia, Greece, India, United_States_of_America, Turkey.
The MAPE is around 20% - 30%, which is mediocre.

## References

> Brownlee, J. (2020, August 14). Autoregression Models for Time Series Forecasting With Python. Retrieved October 11, 2020, from <https://machinelearningmastery.com/autoregression-models-time-series-forecasting-python/>
