I recently worked on a project in which a LSTM model predicts weather on a given date by the user. It fetches the data of the previous 30 days from the meteostat api, inputs that into the model to get a weather prediction for the requested date.
Find the source code at https://github.com/sainiarjun/WeatherPredictor.git
## Specifications
- The model uses dataset from meteostat api for fetching the the 30 days dataset on request from user and for creating the main dataset on which the model was trained
- The model is trained on data from 1973 till 2024 i.e around 50 years
- The variables used and predicted are average temperature, minimum temperature, maximum temperature, precipitation, snow, wind speed and atmospheric pressure
- The model uses:
	- Quantile transformer for scaler
	- Mean absolute error (L1 loss) instead of Mean Square error (L2 loss)
	- RMSprop  base optimizer with Lookahead optimizer 
	- A high learning rate of 1 was chosen with learning rate scheduler
	- The model was trained for 20 epochs
- The above choices were made using trial and error trying out different options for each attribute and choosing the best performing one in this usecase
- These are the stats for the best model achieved:
	- Validation Loss: 2.0105
	- RMSE: 20.9647 
	- MAE: 2.0174 
	- R²: 0.6361 
	- Explained Variance Score: 0.6438
	- Average Train loss for first epoch: 78.3053
	- Average Train loss for last epoch (20th): 3.5663
	- Best Average Train loss achieved (for 18th epoch): 3.5606
## Limitations 
- The model only gives prediction for New York currently
- It can only predict for dates for which data for previous month is available i.e all days up to today, making it only useful to predict today's weather 

## Overcoming Limitations
- More locations can be added if data for them is available
- Predictions further into the future can be made if the data for previous 30 days is predicted as well however, this will lead to compounding of errors 
