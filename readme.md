
### Description
As part of the energy valuation activity on the electricity markets, Elmy would 
like to have a forecasting model to judge in advance whether electricity 
prices on the SPOT market (European auction market allowing electricity 
to be purchased the day before for the next day) will be higher or lower 
than electricity prices on the Intraday market (European stock market 
allowing electricity to be purchased the same day).

### Goals
The exercise consists in the supervised modeling of the price gap between 
the intraday market (called "Intraday") and the SPOT market. The price gap 
can be modeled by a regression but also by a classification because what 
matters above all is to correctly predict the direction of this gap (whether 
this or that price will be higher or lower than the other).

### Data description
Index
- DELIVERY_START: date and time of electricity delivery

Explanatory variables
- **load_forecast**: forecast of total electricity consumption in France
- **coal_power_available, gas_power_available, nucelear_power_available**: total 
electricity production capacity of coal, gas and nuclear power plants respectively,
- **wind_power_forecasts_average, solar_power_forecasts_average**: average of 
different forecasts of total wind and solar electricity production (respectively),
- **wind_power_forecasts_std, solar_power_forecasts_std**: standard deviation of 
these same forecasts,
- **predicted_spot_price**: SPOT electricity price prediction from an internal 
Elmy model. This model is launched every day before the SPOT auction closes for the 
next day.

Target variable
- spot_id_delta: the difference between the VWAP of transactions on the intraday 
market and the SPOT price for 1MWh of electricity (spot_id_delta = Intraday - SPOT): 
if the value is positive, the Intraday price is higher than the SPOT price and vice versa.

### Benchmark description
A simple benchmark is to predict that prices on the Intraday market will always 
come out higher than prices on the SPOT market. That is to say that the predicted 
values will always be positive. We observe that, historically, prices on the intraday 
market come out a little more often above prices on the SPOT.

### Model Performance Evaluation Metrics
Since the objective is above all to correctly predict the direction of the deviation, 
we will rely on a classification metric to evaluate the performance of a model. The size 
of the observed deviation is also important to us: the larger the observed deviation, 
the more important it is to correctly predict its direction. The performance metric 
proposed for this challenge is therefore the Weighted Accuracy . That is to say the 
proportion of predictions whose directions (positive or negative) are correctly identified
weighted by the absolute value of the deviations actually observed.