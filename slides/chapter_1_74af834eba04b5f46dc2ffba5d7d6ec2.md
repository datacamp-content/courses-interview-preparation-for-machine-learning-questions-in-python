---
title: Insert title here
key: 74af834eba04b5f46dc2ffba5d7d6ec2

---
## Null RMSE

```yaml
type: "TitleSlide"
key: "cdd8593aee"
```

`@lower_third`

name: Sai Charan Tej
title: Product Manager


`@script`
In the previous lesson, you have learnt how to check for overfitting in your model. Now in this lesson, we are going to answer one of the basic ML Interview questions - How do you benchmark your model?


---
## Exercise

```yaml
type: "FullSlide"
key: "2a96d7ae22"
```

`@part1`
I will benchmark my model by comparing my model's RMSE with the RMSE of:

a.A new model with a different set of input features  

b.A model that always predicted the average 

c.A model that always predicted the correct value 

d.A model that always predicted the wrong value


`@script`



---
## How do you benchmark the model you have built?

```yaml
type: "TwoColumns"
key: "84f6b5b099"
```

`@part1`
Interviewer:The RMSE value of your base model is 164.637 {{1}}

**Does this RMSE value represent a good model or a below-average model?** {{2}}

Let us find out by benchmarking your model! {{3}}


`@part2`
![](https://assets.datacamp.com/production/repositories/4715/datasets/ec28afc57ce07e13b522943efdb57104fe8a1c7c/benchmark.jpg){{2}}


`@script`
The interviewer looks at the RMSE value of your base_model and asks "How good really is your model? Does the RMSE value represent a good model or an average model?" You answer these questions by performing model benchmarking!


---
## What exactly is model benchmarking?

```yaml
type: "TwoColumns"
key: "5a78ebdebb"
```

`@part1`
- You compare your base model's performance with that of a (**stupid**) model that predicts the output without the help of input features. {{1}}

- The RMSE of this stupid model is called 'Null RMSE' {{2}}

- Any machine learning model you build should do better than this stupid model. {{3}}


`@part2`
![](https://assets.datacamp.com/production/repositories/4715/datasets/3ac7f429f4b159a6ba51d31dc9a5e3458285d25b/benchmark-rmse.jpg){{2}}


`@script`
What is model benchmarking?
You compare your model’s performance with that of a stupid model. What is a stupid model? A model that predicts the output without considering input features. I call this model stupid, since it is practically trying to make predictions without considering data.You calculate the RMSE of this stupid model,that is called null_RMSE. Any machine learning model you build should always have its RMSE value lower than null_RMSE for regression problems.Now you must be wondering, how does a stupid model make predictions?


---
## How do you build a stupid model?

```yaml
type: "FullSlide"
key: "fd5681da11"
```

`@part1`
![](https://assets.datacamp.com/production/repositories/4715/datasets/de426914547a8980eddb150374b758d26553d0ee/output.png)


`@script`
Let us find out.How do you make predictions about the total no.of bikes rented when you do not have access to any of the input features?


---
## How does a stupid model predict?

```yaml
type: "FullSlide"
key: "b00e10b99a"
```

`@part1`
If you are to tell the owner of the bikestore, the number of bikes that are going to be rented in the next hour, which of the below estimates will you choose?

a.Random Guess 

b.Average number of bikes rented per hour 

c.Max number of bikes rented per hour 

d.Min number of bikes rented per hour 

**Answer: b ** {{1}}


`@script`
If you are to go to the bikestore owner and come up with a prediction about the no.of bikes that are going to be rented in the next hour, which of these measures would you choose? You should choose option B,average no.of bikes rented per hour.


---
## Why does predicting the mean make sense?

```yaml
type: "TwoColumns"
key: "6e6a7d7210"
```

`@part1`
- Central Tendency states that majority of values in a distribution lie around the center. {{1}}
- This is the best prediction you can make in the absence of input features {{2}}


`@part2`
![](https://assets.datacamp.com/production/repositories/4715/datasets/31602aabca0fa5fb0ddd86bcff7bd91c2f2c0d82/central-tendency-copy.jpg){{1}}


`@script`
You must be thinking why does predicting the mean make sense?
Central tendency. According to central tendency, majority of the values in a distribution lie around the center and in the absence of input features, a central tendency measure like mean is your best bet.This is exactly what a stupid model does. It chooses a central tendency measure like average as its prediction.


---
## Benchmarking

```yaml
type: "FullSlide"
key: "cf60a44c5a"
```

`@part1`
Below are the steps to benchmark your model:

1.Split the data into training data and test data

2.Calculate the Average Number of Bikes Rented every hour for the test data. This becomes the prediction of the stupid model.

3.Calculate the Null RMSE value by taking into consideration these predictions

4.Verify whether your base model's RMSE value is lower than Null RMSE or not


`@script`
Now that we know how a stupid model makes predictions, let us formally define the process for benchmarking.These are the 4 steps in the benchmarking process. Let us look at each of the steps in detail.


---
## Step 1: Split the data into training and test data

```yaml
type: "FullSlide"
key: "2928632209"
```

`@part1`
```python
# split X and y into training and testing sets
X_train, X_test, y_train, y_test = 
train_test_split(X, y, random_state=3)```


`@script`
Step1: You split the data into training and test data just like how you split the data while building your base_model


---
## Step 2: Calculate the mean response value

```yaml
type: "FullSlide"
key: "a3a5996483"
```

`@part1`
We create and fill an array **y_null** with the average number of bikes rented per hour
```python
# create a NumPy array with the same shape as y_test
y_null = np.zeros_like(y_test, dtype=float)

# fill the array with the mean value of y_test
y_null.fill(y_test.mean())
print(y_null)
```
**Output:** [190.732,190.732,......190.732]


`@script`
You initialize an array y_null and fill it with the average of the output variable in the test data for all the test samples. This y_null array represents the predictions of your stupid model.


---
## Step 3: Calculate Null RMSE

```yaml
type: "FullSlide"
key: "fff65c249c"
```

`@part1`
```python
# fill the array with the mean value of y_test
y_null.fill(y_test.mean())
# compute null RMSE
null_rmse = np.sqrt
(metrics.mean_squared_error(y_test, y_null))
print (null_rmse)
```
**Output:** 180.448


`@script`
You calculate the RMSE of this stupid model just like how you calculated RMSE value for your base_model. The only difference is instead of y_pred,you have y_null which is nothing but the predictions of the stupid model.


---
## Step 4: Benchmark your model against Null RMSE

```yaml
type: "FullSlide"
key: "16e00dbbc0"
```

`@part1`
Now you can compare the **RMSE value of your base model** against the **null_rmse**.
```python
if rmse_base_model < null_rmse:
 print('Your model is better than a stupid model')
else:
 print('Your model is worse than a stupid model')
```
**Output:** You model is better than a stupid model


`@script`
Finally, you verify if your base_model’s RMSE is lower than null_RMSE or not. If the base_model's RMSE is lower, then congratulations, your model is a good model.You have used machine learning to better predict the output. If it is not, if your base_model's RMSE is higher than null RMSE, then you have built a model so bad that it would have made more sense if you did not build a model in the first-place.Your base_model's RMSE should always be less than null_RMSE. That's how you benchmark your base_model.


---
## Exercise - Solution

```yaml
type: "FullSlide"
key: "bfe4077f6e"
```

`@part1`
I will benchmark my model by comparing my model's RMSE with the RMSE of:

a.A new model with a different set of input features  

**b.A model that always predicted the average **

c.A model that always predicted the correct value 

d.A model that always predicted the wrong value


`@script`



---
## Summary

```yaml
type: "FullSlide"
key: "28f258b8d7"
```

`@part1`
In order to benchmark your model, you need to:

1.Build a stupid model which predicts the output in the absence of input features using central tendency measures{{1}}

2.Calculate the Null RMSE for this stupid model {{2}}

3.Verify whether your base model's RMSE is above or below the Null RMSE {{3}}


`@script`
To summarize, when the interviewer asks you 'What is the best way to benchmark your model?' you need to:
1.First build a stupid model which predicts the output using central tendency measures
2.Then calculate the RMSE value of this stupid model.
3.Finally you verify whether your base_model's RMSE is lower than this null_rmse or not.
This is how you benchmark your model.Thanks for watching!


---
## Let's practice!

```yaml
type: "FinalSlide"
key: "41126c3cf3"
```

`@script`


