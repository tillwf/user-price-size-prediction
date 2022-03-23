## Initial problem

Personalisation matters for us. For this purpose we collected `product_view` and `purchase` events. As an applied scientist in the Recommendation & Personalisation team, we kindly ask you to analyse events and try to predict for every user `size` and `price` preferences. Those preferences can be a range or directly a value. You can chose the response data structure.

(Optionally) If you want you can also add how certain is your prediction per user and property.

## Input Data Format

`events.log` file is in JSONL format. Every row has an event serialized as json with the properties:
{
    "user_id": used id of the event,
    "event": name of the event, (`product_view` or `purchase`)
    "price": price of the product,
    "size": size of the product
}

## Installation

```
pip install -U pip
pip install -r requirements.txt
```

The data file `events.log` should be placed in the folder `data/`

## Description of the solution

The notebook `exploration.ipynb` mixes the data analysis and the solution proposed for the current problem.

To sum up the analysis results, we observed that the data seems chronologically displayed. This means that when a purchase occurs, the previous views can be considered as historical data for this purchase. This is why we used this `purchase` events to split users actions into sessions.

### Sizes prediction

For the sizes, the idea was to estimate the probability of buying a specific `size` using a beta distribution. Each user would have 4 distributions (one per size), and the parameters `a` and `b` of each distribution would be calculated using the number of event per size.
With these distributions, we can sample probabilities for each size and observe which one is the most probable. Averaging this probabilities gives us a probability of liking a specific size. The idea, borrowed from Thompson Sampling for Contextual Bandits, allow us, if there is some king of size recommendation, to exploit and explore and thus increase our knowledge of each users. This also help us handle evolution of taste in time.

### Prices prediction

#### Simple solution

The simple solution consists in averaging all the prices observed and its standard deviation. We then construct a range of price using `mean - std` and `mean + std`. With lots of close price, the range will be small, and with few sparse prices, the range will be big. The problem comes from multiple sessions and unique data input (no deviation).

#### Beginning of a more complex solution

The more complex solution is to estimate the likelihood of the gaussian parameters which could describe best the data. Using this likelihood function we could then compute a posterior function to get a prediction of the parameters, but currently we are just extracting the parameters that fit the most to the data (which is approximatively the real mean and the real variance).

### Output

The size preferences will be outputed in `data/size_predictions.json` and the price preferences in `data/price_predictions_simple.json`.

## Future work

With more time we could have:

 - Used the purchase events to enforce or even change our predictions
 - Used the session as it can indicate different usage (maybe buying a gift)
 - Computed real confidence interval for the prices

