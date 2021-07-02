Forecast model selection for PM2.5 levels in China :                                                          
Introduction
The purpose of this notebook is to create an appropriate model to forecast PM2.5 levels in China. It is a time series forecasting project.
Methodology
•	First csv file "BeijingPM20100101_20151231.csv" is selected for in depth analysis and converted to data frame.
•	The "year", "month", "day”, “hour" is converted to one date time format.
•	All the features 'TEMP','PRES','DEWP','HUMI','Iws','PM25','precipitation','Iprec' are plotted to see a trend/variation through time.
•	A plotly express plot for PM2.5 is applied to visualize the data in depth.
•	From the feature visualization analysis,  features selected for the time series model
•	The Multi variate time series model using Deep learning LSTM (Long short-term memory) sequence model worked well by including 4 dependent/correlated features, namely Dew Point, Temperature, Pressure and Cumulated wind speed for predicting PM2.5 in Beijing city.
•	The NaN values in all the features and the PM2.5 values were filled with forward fill method.
•	The complete data frame was scaled by MinMaxScaler method.
•	The TimeseriesGenerator method is employed to feed the data in the Deep Neural network architecture.
•	The complete dataset is split into train and test with 80 to 20 % ratio without shuffle=False, as the time consistency is important in the time series analysis
•	The model consists of Sequential layer with 2 LSTM layer followed by LeakyReLU and then followed by 2 Dropout Layer with a LSTM layer in between and finally the dense layer. 
•	The model consists of 5 features including the PM2.5 with a window length =120. This window is for 5 days and as each day has 24 data points.
•	The batch size is 32. The hyperparameters were tuned several times to get a good fit.
•	The model was trained for 50 epochs. 
•	The method of early stopping was applied, and the model worked well and stopped in the 4th epoch.
•	The training mean absolute error is 0.0164.
•	The model was evaluated with test data.
•	The predicted value was evaluated by test generator.
•	The inverse of the scaling method is applied to get the real value of PM2.
•	The actual PM2.5 and the predicted PM2.5 value is in well agreement.
•	The plot shows the good overlap of the PM2.5 actual value and the predicted value.
•	The model metrics for the performance is further checked with the linear correlation plot. 
•	The calculated and predicted values are in good agreement for PM2.5 values less than 500 and is scattered for values greater than 500.
Conclusions
•	With my few experiences in time series data analysis, I felt, I got more flexibility to tune the hyperparameter in the Deep learning LSTM (Long short-term memory) sequence model. 
•	Although the Autoregressive integrated moving average (Auto-ARIMA) model and the Facebook’s Prophet model was tried but with not much success.

•	The data is analyzed only for the Beijing city. The model performance can be checked for other 4 cities for a better decision.
•	The 'Combined wind direction' feature being in the string format was neglected. The PM2.5 value is dependent in the wind direction. It would have been good if this feature was also included by changing it to  a parameter that fits to feed the model.
•	The data is not limited, with 52584 data points a model with good performance can be build.
•	We had to drop the first few (24 data points) because of forward fill method. Other method can be applied like backward fill, etc. to include those data points.
•	The model does not look overfitted, but it misses to get the higher values of PM2.5. These higher values should be checked if they are outliers or really Beijing city gets this high value.
•	The LSTM sequential model can be applied to forecast the PM2.5 values in China with further insights as stated above.
