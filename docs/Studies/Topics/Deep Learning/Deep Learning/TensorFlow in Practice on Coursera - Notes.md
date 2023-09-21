---
share: "true"
---
# TensorFlow in Practice on Coursera Notes

The following are Daniel Bourke's (me) notes from going through the [TensorFlow in Practice Specialization on Coursera](https://dbourke.link/tfinpractice) in preparation for the TesnorFlow Developer Certification.

Full curriculum:

[[Getting TensorFlow Developer Certified Curriculum|Getting TensorFlow Developer Certified Curriculum]]

**Game plan:** go through lectures, don't take many notes, focus on the practice. Code. Code. Code. I'm not focused on passing the Coursera course, more so getting skills to the pass the TensorFlow Developer Certification.

---

## Key

- 🔑 = Major key, something to remember and come back to
- 📖 = Extra resource or reading
- 🚫 = Error/issue

## Log

**Start:**  May 11, 2020

**Finish:** May 27, 2020

There are four parts to the full Specialization:

1. Introduction to TensorFlow for Artificial Intelligence, Machine Learning and Deep Learning

    **Started:** May 11, 2020

    **Finished:** May 12, 2020

2. Computer vision with TensorFlow

    **Started:** May 13, 2020

    **Finished:** May 15, 2020

3. Natural language processing with TensorFlow

    **Started:** May 18, 2020

    **Finished:** May 21, 2020

4. Time series and structured data prediction with TensorFlow

    **Started:** May 22, 2020

    **Finished:** May 27, 2020


I'll work through each part at about 1 week per part.

---

## Part 4 — Sequences, Time Series and Prediction

### Week 1 — Sequences and Prediction

May 22, 2020

- Time series data is data which is created over a time period, for example, the demand of taxi cabs at certain hours of the days, higher when people finish work at 5pm but lower when people are asleep at 2am.
- One important thing to remember is the difference between creating train, valid and test sets with time series.
    - Splitting the traditional way (random shuffle of 70/15/15) can lead to incorrect splits.
    - This is because, most of the time, you'll be wanting to use previous time series data to predict future time series data.
- There are two main types of time series data:
    1. Univariate time series — only one parameter through time, such as, video game sales over time.
    2. Multivariate time series — multiple parameters through time, such as, birth and death rates.
- Applications for machine learning in time series include:
    - Anomaly prediction — finding a sample which shouldn't have occurred in a series of other samples over time.
    - Forecasting — predicting future events based on past events.
    - Analyzing sequences to recognize what called them — predicting what word a soundwave produced based on the timesteps of the wave.
- Types of time series in the wild include:
    - Trend — something going in a certain direction and assumingly going to keep going in that direction.
    - Seasonality — events which follow other events, such as, the amount of people at a shopping centre on the weekend versus during the week.
    - Autocorrelation — timesteps which are very similar to previous timesteps but don't appear to have a defined trend.
    - Noise — unpredictable occurrences scattered across time.
        - Many real-world datasets will have some level of each of these.
- 🔑 If you're forecasting on time series data, you'll want to split your data into a training period (the first 70% of time steps), a validation period (the next 15% of the time steps) and a testing period (the final 15% of the time steps).
    - You can then use these splits to train on past data and predict on new (the test set will be new to the model) data and then compare how your model's predictions compared to the actual events in the test data.
    -

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.26.34_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.26.34_am.png]]

Different data splits examples for forecasting.

- Another option for creating train, valid and test splits for time series data is to use roll-forward partitioning. This involves:
    - Start training on the earliest data, gradually increasing as needed.
    - Your validation data are the most recent examples, where as, your test period are the timestamps happening now and into the future.
    - This means your model gets evaluating on a rolling basis as new data flows in.

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.31.12_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.31.12_am.png]]

Example of roll-forward partitioning data splitting for time series data.

- 🔑 Different metrics for evaluating time series include:
    - `errors = forecasts - actual`
    - `mse = np.square(errors).mean()`
        - Squaring errors gets rid of negative errors.
    - `rmse = np.sqrt(mse)`
        - Taking the square root gets the MSE into the same scale as your data.
    - `mae = np.abs(errors).mean()`
    - `mape = np.abs(errors/x_valid).mean()`
        - This gives an idea of the size of the error compared to the size of the values.
    - If large errors are worse than smaller errors, choose MSE but if your errors (large or small) are all the same, choose MAE.
- Example of calculating the MAE (mean absolute error) using Keras:

```python
keras.metrics.mean_absolute_error(x_valid,
																	naive_forcast).numpy()
>>> some_error_value

```

- 🔑 Simple approaches such as smoothing both the past and present values can lead to great results before approaches such as deep learning:
    - For example, you could try: Forecasts = trailing moving average of differenced series + centred moving average of past series (t - 365).
    - **Moving average** involves taking a box of values (for example the pat 30 days) and using the mean of these values as the next time step prediction. This eliminates a lot of noise but does not include trend or seasonality.
    - **Differencing** involves the studying the time series with no trend or seasonality.
        - You can do this using Series(t) - Series(t-365)
- Example of moving average:

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.45.45_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-22_at_10.45.45_am.png]]

Moving average uses a moving window along a small series of time using the mean of the moving window as the next step prediction.

- Start with a simple way to predict a time series, such as, moving average windows and differencing then see if machine learning can beat it.
- 📖 **Questions**
    - What is an example of a univariate time series?
        - Hour by hour temperature.
    - What is an example of a multivariate time series?
        - Hour by hour weather.
    - What is imputed data?
        - A projection of unknown (usually past or missing) data.
    - Is a sound wave a good example of time series data? Why?
        - Yes, because it contains multiple pieces of information across time. For example, a 44kHz soundwave has 44,000 pieces of information per second.
    - What is seasonality?
        - A regular change in shape of the data.
    - What is a trend?
        - An overall direction for data regardless of direction.
    - In the context of time series data, what is noise?
        - Unpredictable changes in the time series data.
    - What is autocorrelation?
        - Data that follows a predictable shape, even if the scale is different.
    - What is a non-stationary time series?
        - One that has a disruptive event breaking trend and seasonality.

### Week 2 — Deep Neural Networks for Time Series

May 25, 2020

- One of the most important hyperparameters to tune for a deep learning model is the learning rate. Fortunately, there are several ways to automate this.
- Machine Learning on Time Windows (sequences of data):
    - As always you've got to split your data into data (X) and labels (y). In this case, the data is a sequence of timesteps before the label.

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-25_at_9.50.35_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-25_at_9.50.35_am.png]]

Example of creating data and labels for a time window.

- Using the `tf.Data.Dataset()` API, you can shuffle your dataset with the `.shuffle()` method, passing it the parameter `buffer_size` for the amount of data you'd like to shuffle.
- Example of creating a sliding window shuffled data with `tf.data.Dataset()`:

```python
# Create the dataset
dataset = tf.data.Dataset.range(10)
# Create the data windows (size 5)
dataset = dataset.window(5, shift=1, drop_remainder=True)
# Create batches
dataset.flat_map(lambda window: window.batch(5))
# Map the X & y values (X = all but last, y = last)
dataset = dataset.map(lambda window: (window[:-1], window[-1:]))
# Shuffle the dataset
dataset = dataset.shuffle(buffer_size=10)
# Check the X & y values
for x, y in dataset:
	print(x.numpy(), y.numpy())

>>> [3 4 5 6] [7]
>>> [4 5 6 7] [8]
>>> [1 2 3 4] [5]
>>> [2 3 4 5] [6]

## You can also batch the datasets
# ...same code as above...
dataset = dataset.batch(2).prefecth(1)
for x, y in dataset:
	print("x = ", x.numpy())
	print("y = ", y.numpy())

# We get batches of size 2 (2 x X's, 2 x y's)
>>> x = [[4 5 6 7] [1 2 3 4|4 5 6 7] [1 2 3 4]]
>>> y = [[8] [5|8] [5]]
>>> x = [[3 4 5 6] [2 3 4 5|3 4 5 6] [2 3 4 5]]
>>> y = [[7] [6|7] [6]]

```

- 🔑 Sequence bias — If you're giving a list of things and asked to picked which is your favourite, chances are you'll pick the first one (if you're familiar with it). You don't want this bias coming into the training data, so it's a good idea to shuffle things up. But make sure they keep their times series order.
- A single layer neural network (with one dense layer) with a single neuron is equivalent to a linear regression model.
- Example of making predictions with a model on time series:

```python
series[1:21] = [49.375, 53.312, 57.899...]

# Make predictions on a series of data, use np.newaxis to reshape to correct output size
model.predict(series[1:21][np.newaxis])

>>> array([[49.08478|49.08478]], dtype=float32)
```

- 🔑 This lecture goes through techniques to find the ideal learning rate for a model: [https://www.coursera.org/learn/tensorflow-sequences-time-series-and-prediction/lecture/HecKT/deep-neural-network-training-tuning-and-prediction](https://www.coursera.org/learn/tensorflow-sequences-time-series-and-prediction/lecture/HecKT/deep-neural-network-training-tuning-and-prediction)
    - The technique is to train a model with a learning rate scheduler to gradually increase the learning rate and then to plot the learning rate versus the model loss.
    - You'll get a curve back. Take the bottom of this curve and go back an order of magnitude (just before the very bottom) and that's your ideal learning rate (the point at which the loss is getting lower but isn't at rock bottom yet).
- Example of how to find the best learning rate using `tf.keras.callbacks.LearningRateScheduler()`:

```python
# Create the learning rate scheduler callback
lr_scheduler = tf.keras.callbacks.LearningRateScheduler(
	lambda epoch: 1e-8 * 10**(epoch/20))

# Add the callback to the fit() fuction
history = model.fit(..., ..., callback=[lr_scheduler])

# When you get the results, plot the learning rate against the loss
lrs = 1e-8 * (10 ** (np.arange(100)/20))
plt.semilogx(lrs, history.history['loss']) # plot a plot with a log scale along x
plt.xlabel("Learning rate")
plt.ylabel("Loss")
plt.axis([1e-8, 1e-3, 0, 300])
```

- 🔑 Once you get the learning rate versus loss plot, take the learning rate a few steps away from lowest loss value (e.g. if the lowest loss value falls on 10e-5, you'll probably want to take 7e-6).

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-25_at_4.32.17_pm.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-25_at_4.32.17_pm.png]]

Example of plotting the loss versus the learning rate to find the ideal learning rate. Notice the x-axis is on a log scale. The ideal learning rate is a few steps to the left of the bottom of the curve (in this case, about 8e-6, where the loss is still decreasing but isn't unstable like at 10e-5).

- 📖 **Questions:**
    - What is a windowed dataset?
        - A fixed-sized subset of a time series.
    - What does `drop_remainder=True` do?
        - It ensures that all rows in the data window are the same length by cropping data.
    - What code can be used to split an n column window in n-1 columns for features and 1 column for a label:
        - `dataset = dataset.map(lambda window: (window[:-1], window[-1:]))`
    - What does MSE stand for?
        - Mean squared error
    - What does MAE stand for?
        - Mean absolute error
    - If time values are in `time[]` and series values are in `series[]` and we want to split the series into training and validation at time 1000, what the is the correct code?

```python
time_train = time[:split_time]
x_train = series[:split_time]
time_valid = time[split_time:]
x_valid = series[split_time:
```

- If you want to inspect the learn parameters in a layer after training, what's a good technique to use?
    - Assign a variable to the layer and add it to the model using that variable. Inspect its properties after training.
- How do you set the learning rate of the SDG optimizer?
    - Use the `lr` parameter.
- If you want to amend the learning rate of the optimizer on the fly, after each epoch, what do you do?
    - Use a `LearningRateScheduler` object in the callbacks namespace and assign that to the callback when training.

### Week 3 — Recurrent Neural Networks for time series (LSTMs for time series)

May 26, 2020

- LSTMs and recurrent neural networks should be able to capture pieces of information in sequences which whose importance are based on their position, for example: a recent event may be more predictive of a new event than an event which happened a a while ago.
- 🔑 In Keras, Lambda layers allow you to write arbitrary pieces of code (like preprocessing functions) into the model itself.
    - Rather than writing a scaling function on its own, you can create it as part of the network itself.
- In Keras, when stacking one RNN on top of another, the default behaviour is to output a vector (sequence-to-vector).
    - If you want RNN layers in Keras to return sequences, you have to set `return_sequences=True` in the layer.

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.44.12_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.44.12_am.png]]

The default behaviour in Keras of a recurrent layer is to output a vector rather than a sequence. So be sure to set return_sequences=True if you're stacking recurrent layers.

- Overview of an unrolled recurrent layer:

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.40.49_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.40.49_am.png]]

A recurrent layer takes X as input and outputs Y. In between cells it passes the hidden state of the previous cell to the next.

- At each time step, the memory cell gets the current input as well as the previous cells hidden state:

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.43.08_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-26_at_9.43.08_am.png]]

- For inputs to an RNN layer, TensorFlow assumes the first dimension is the batch size and the second dimension can be any size at all (any length of sequences), the final dimension is how many variates in the time series.
    - For example: `input_shape=[32, None, 1]` defines an input with a batch size of 32, an arbitrary number of timestamps (None) and is univariate (1).

```python
# Example simple RNN model in Keras
model = keras.models.Sequential([
	keras.layers.SimpleRNN(20,
												 return_sequences=True, # returns sequences not vector
												 input_shape=[None, 1]), # (batch_size, no. timestamps, no. variates (this one is univariate))
	keras.layers.SimpleRNN(20, return_sequences=True) # outputs sequence
	keras.layers.Dense(1)
])
```

- The default activation function in RNN layers is `tanh()` and this outputs values between -1 and 1.
- Example of Lambda layers (layers which can perform arbitrary operations such as data preprocessing) in a Keras model:

```python
model = keras.models.Sequential([
	keras.layers.Lambda(lambda x: tf.exapnd_dims(x, axis=-1),
											input_shape=[None]), # input shape accepts series of any length
	keras.layers.SimpleRNN(20, return_sequences=True),
	keras.layers.SimpleRNN(20),
	keras.layers.Dense(1),
	keras.layers.Lambda(lambda x: x * 100.0)])
```

- The Huber Loss function is a combination of MSE and MAE, it's less sensitive to outliers. You can use it in TensorFlow with: `tf.keras.losses.Huber()`
- Example of setting up a model with a learning rate scheduler to find the ideal learning rate for training:

```python
model = tf.keras.Sequential([
	tf.keras.layers.Lambda(lambda x: tf.expand_dims(x, axis=-1), input_shape=[None]),
	tf.keras.layers.SimpleRNN(40, return_sequences=True),
	tf.keras.layers.SimpleRNN(40),
	tf.keras.layers.Dense(1),
	tf.keras.layers.Lambda(lambda x: x * 100.0) # rescale the values into the 10s
])

# Create learning rate schedule
lr_scheduler = tf.keras.callbacks.LearningRateScheduler(lambda epoch: 1e-8 * 10**(epoch / 20))

# Set up the optimizer
optimizer = tf.keras.optimizers.SGD(lr=1e-8, momentum=0.9)

# Compile the model with Huber loss
model.compile(loss=tf.keras.losses.Huber(),
							optimizer=optimizer,
							metrics=['mae'])

history = model.fit(train_set, epochs=100, callbacks=[lr_schedule])
```

- After running the above, plot the loss vs. the learning rate and see what learning rate the loss is at its lowest. Use that new learning rate to train your model.
- Bidirectional LSTMs mean the cell state gets passed forward and backward through the sequences.
- Example of building a multi-layer LSTM model for time series data:

```python
# Clear the previous saved variables from the session
tf.keras.backend.clear_session()

# Create a dataset
dataset = windowed_dataset(x_train, window_size, batch_size, shuffle_buffer_size)

# Setup a model
model = tf.keras.Sequential([
	tf.keras.layers.Lambda(lambda x: tf.expand_dims(x, axis=-1),
												 input_shape=[None]),
	tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32, return_sequences=True)),
	tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32)),
	tf.keras.layers.Dense(1)
	tf.keras.layers.Lambda(lambda x: x * 100.0)])

# Compile the model
model.compile(loss='mse',
							optimizer=tf.keras.optimizers.SGD(lr=1e-6, momentum=0.9))
model.fit(dataset, epochs=100)
```

- 📖 **Questions**
    - If X is the standard notation for the input to an RNN, what are the standard notations for the outputs?
        - Y(hat) (ouputs) and H (hidden state).
    - What is a sequence-to-vector output if an RNN has 30 cells numbers 0 to 29?
        - The Y(hat) for the last cell.
    - What does a Lambda layer in a neural network do?
        - Allows you to execute arbitrary code while training.
    - What does the axis parameter of `tf.expand_dims` do?
        - Defines the dimension index at which you will expand the shape of the tensor. See: [https://www.tensorflow.org/api_docs/python/tf/expand_dims](https://www.tensorflow.org/api_docs/python/tf/expand_dims)
    - What loss function combines MAE and MSE? Why is it useful?
        - Huber loss is stable to outliers and differentiable (important for gradient descent to work).
    - What is the primary difference between a simple RNN and an LSTM?
        - In addition to the H (hidden state) output, LSTMs have a cell state that runs across all cells.
    - If you want to clear out all temporary variables that TensorFlow might have from previous sessions, what code do you run?
        - `tf.keras.backend.clear_session()`
    - What happens if you define a neural network with these two layers?

    ```python
    tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32)),
    tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32)),
    tf.keras.layers.Dense(1)...

    # Your model will fail because you need return_sequences=True after the first LSTM layer
    # return_sequences=True should be on when stacking LSTMs
    ```


### Week 4 — Real-world time series data

May 27, 2020

- This week we're going to look at modelling time series data with an RNN as well as a Convolutional Neural Network.
- Example of creating a model with LSTMs and and a 1D CNN:

```python
model = tf.keras.models.Sequential([
	tf.keras.layers.Conv1D(filters=32, kernel_size=5, strides=1, padding="casual",
												 activation='relu',
												 # input shape is specified here, so we need to update the data creation function
												 # with tf.expand_dims(x, axis=-1)
												 input_shape=[None, 1]),
	# You can make these bidirectional and see how they go
	tf.keras.layers.LSTM(32, return_sequences=True),
	tf.keras.layers.LSTM(32, return_sequences=True),
	tf.keras.layers.Dense(1),
	tf.keras.layers.Lambda(lambda x: x * 200)])

optimizer = tf.keras.optimizers.SGD(lr=1e-5, momentum=0.9)

model.compile(loss=tf.keras.losses.Huber(),
							optimizer=optimizer,
							metrics=['mae'])

model.fit(dataset, epochs=500)
```

- To improve the efficiency of your neural network training, try mini-batch gradient descent:

[https://www.youtube.com/watch?v=4qJaSmvhxi8](https://www.youtube.com/watch?v=4qJaSmvhxi8)

- 1 epoch = 1 single pass through the training set (forward and backward propagation).
- To skip the first row in a CSV (usually headers), use something like:

```python
import csv

with open('some_csv_file.csv') as csvfile:
	reader = csv.reader(csvfile, delimiter=',')
	next(reader) # Skip the first row (get the 'next' item in the iterable)
	for row in reader:
		#...append labels
	  #...append data
```

- Remember when starting training, try a simple model (like a DNN first) before trying a more complicated model (like a multi-layer RNN with LSTMs).
- Example of creating a model with Conv1D, 2 LSTMs and a DNN as output:

```python
model = tf.keras.models.Sequential([
	tf.keras.layers.Conv1D(filters=32, kernel_size=5,
												 strides=1, padding="casual",
												 activation="relu",
												 input_shape=[None, 1]),
	tf.keras.layers.LSTM(32, return_sequences=True),
	tf.keras.layers.LSTM(32, return_sequences=True),
	tf.keras.layers.Dense(30, activation='relu'),
	tf.keras.layers.Dense(10, activation='relu'),
	tf.keras.layers.Dense(1),
	tf.keras.layers.Lambda(lambda x: x * 400)]) # get outputs to between 0 and 400
```

- 📖 **Questions — 1844 learners**
    - How do you add a 1-dimensional convolution to your model for predicting time series data?
        - Use a `tf.keras.layers.Conv1D()` layer.
    - What's the input shape for a univariate time series to a Conv1D?
        - `input_shape = [None, 1]`
    - What's the name of the Python library used to read CSVs?
        - `csv`, import using `import csv`
    - If you're CSV file has a header that you don't want to read into your dataset, what do you execute before iterating through the file if your data is stored in the `reader` object?
        - Use `next(reader)` to skip the first row.
    - When you read a `row` from a `reader` and want to cast column 2 to another data type, for example, a float, what's the correct syntax?
        - `float(row[2)`.
    - What neural network type do you think is best for predicting time series data?
        - It depends. But a combination of DNN, convolutions and RNN/LSTMs generally works well.
    - Why is MAE a good metric for measuring accuracy of predictions for time series?
        - It doesn't heavily punish larger errors like square errors do.
        - You get an idea of the exact difference each prediction is from the actual label.

**Next**

- [x]  Go through Week 4 Lesson 1 — [https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow In Practice/Course 4 - S%2BP/S%2BP Week 4 Lesson 1.ipynb](https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow%20In%20Practice/Course%204%20-%20S%2BP/S%2BP%20Week%204%20Lesson%201.ipynb)
- [x]  Go through Week 4 Lesson 5 notebook — [https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow In Practice/Course 4 - S%2BP/S%2BP Week 4 Lesson 5.ipynb](https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow%20In%20Practice/Course%204%20-%20S%2BP/S%2BP%20Week%204%20Lesson%205.ipynb)
- [x]  Go through Week 4 exercises — [https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow In Practice/Course 4 - S%2BP/S%2BP Week 4 Exercise Question.ipynb](https://colab.research.google.com/github/lmoroney/dlaicourse/blob/master/TensorFlow%20In%20Practice/Course%204%20-%20S%2BP/S%2BP%20Week%204%20Exercise%20Question.ipynb)

---

## Part 3 — Natural language processing with TensorFlow

### Week 1 — Sentiment in text

May 18, 2020

- The first thing when dealing with natural language, the same as when dealing with all other data is to turn it into numbers.
- How do you understand the meaning of a word with numbers? For example, you could take the number of the alphabet each letter occurs and use that string of numbers to understand it.
    - Listen → 12, 9, 19, 20, 5, 14
    - Silent → 19, 9, 12, 5, 14, 20
        - This approach doesn't work that well. These two words have opposite meanings but contain the same numbers.
- What about a word based encodings? For example:
    - I love my dog → 1, 2, 3, 4
    - I love my cat → 1, 2, 3, 5
        - This approach is starting to get better since the first 3 words have the same numbers.
- 🔑 Turning words into numbers is known as **Tokenizing**, Keras includes this functionality in the `Tokenizer` class.

```python
# Example tokenizer code in TensorFlow
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.preprocessing.text import Tokenizer

# Note: Tokenization removes all punctuation
sentences = [
	'I love my cat',
	'I love my dog'
]

tokenizer = Tokenizer(num_words = 100) # too many for this example, but you could set it to the len(vocab)
tokenizer.fit_on_texts(sentences)
word_index = tokenizer.word_index
print(word_index)
```

- To turn text to sequences in Keras use `tokenizer.text_to_sequences()`, this will convert a sequence of text to a sequence of numbers.
    - If the word is missing from the tokenizer, it won't be encoded into the sequence. For example, if you made a tokenizer on "I love my dog" and passed it a new sentence "I really love my dog", the word really would be lost.
    - 🔑 To handle missing words in a vocabulary, you can place in a placeholder such as `OOV` (for **Out Of Vocabulary**) to go in place of missing words.
        - To use an OOV token, use the parameter `oov_token` with the `Tokenizer` class.
- 🔑 **Padding** is used to make sure all sequences are the same length. That way when passed to a neural network, the matrices it accepts as input are all a uniform size.
- Example padding code:

```python
padded = pad_sequences(sequences,
											 padding='post', # add the padding to the end
											 truncating='post', # remove words from the end (if maxlen setup)
											 maxlen=5) # set the maximum length of a sequence (will cause all sequences to be this size)
```

- Creating a tokenizer with out of vocabulary token and padded sequences:

```python
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences

tokenizer = Tokenizer(oov_token="<OOV>")

sentences = [SOME_LIST_OF_SENTENCES]

tokenzier.fit_on_texts(sentences)
word_index = tokenizer.word_index

sequences = tokenizer.texts_to_sequences(sentences)
padded = pad_sequences(sequences, padding='post')
print(padded[0])
print(padded.shape)
```

- 📖 **Questions**
    - What is the name of the object used to tokenize sentences?
        - Tokenizer
    - What is the name of the method used to tokenize a list of sentences?
        - `fit_on_texts(sentences)`
    - Once you have the corpus tokenized, what's the method used to encode a list of sentences to use those tokens?
        - `texts_to_sequences(sentences)`
    - When initializing the tokenizer, how do you specify a token to use for unknown (out of vocabulary) words?
        - `oov_token=<Token>`
    - If you don't use a token for out of vocabulary words, what happens at encoding?
        - The word isn't encoded, and is skipped in the sequence.
    - If you have a number of sequences of different lengths, how do you ensure that they are understood when fed into a neural network?
        - Use the `pad_sequences` object from the `tensorflow.keras.preprocessing.sequence` namespace.
    - If you have a number of sequences of different length, and call pad_sequences on them, what's the default result?
        - They'll get padded to the length of the longest sequence by adding zeros to the beginning of shorter ones.
    - When padding sequences, if you want the padding to be at the end of the sequence, how do you do it?
        - Pass `padding='post'` to `pad_sequences` when initializing it

### Week 2 — Word embeddings

May 19, 2020

- 🔑 **Word embeddings** is a way of turning your words into numbers which is better than simply labelling words in your vocabulary from 1 to 10,000 (if you've got 10,000 different words).
    - They capture the relationships between words as such, King - Man + Queen = Woman.
    - Another example, the vector dog might point in the same direction as the vector canine.
- 📖 Check out [http://projector.tensorflow.org/](http://projector.tensorflow.org/) as a way to visualize different embeddings in feature space.
    - Try searching for different words and see which other words they appear closest to.
- The TensorFlow Data Services (or TFDS for short) has a bunch of datasets in-built and ready to use.

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-19_at_9.14.41_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-19_at_9.14.41_am.png]]

In TFDS (TensorFlow Data Services) you'll find a whole range of example datasets you can use to practice and learn on.

- If you don't have TensorFlow datasets installed (you're working outside of Google Colab), you can install them with:

`!pip install -q tensorflow-datasets`

- Using either a Flatten layer (`tf.keras.layers.Flatten()`) or a GlobalAveragePooling1D (`tf.keras.layers.GlobalAveragePooling1D()`) layer in text processing are often interchangeable.
    - In fact, `tf.keras.layers.GlobalAveragePooling1D()` may be faster.
- Example of building a model with an embedding layer as the first layer:

```python
vocab_size = 10000 # how many unique words in the vocabulary?
embedding_dim = 16 # this is a tuneable parameter
max_length = 120 # how long do you want your max sequences to be?

model = tf.keras.Sequential([
	tf.keras.layers.Embedding(vocab_size, embedding_dim, input_length=max_length),
	tf.keras.layers.Flatten(),
	tf.keras.layers.Dense(6, activation='relu'),
	tf.keras.layers.Dense(1, activation='sigmoid')]) # binary classification (outputs get pushed to 0 or 1)

model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])

# Get the size of the embedding layer
embedding_layer = model.layers[0]
weights = embedding_layer.get_weights()[0]
# outputs the size of the embedding: (vocab_size, embedding_dim)
print(weights.shape) # in other words, an embedding_dim size vector for each word in the vocab
```

- This kind of model will push towards 100% accuracy on the training set which is a strong indication of overfitting.
- 🔑 When you're working with text data, you might find the validation loss increases as training goes on.
    - Think of this as the confidence of the models prediction on a particular sample.
    - One of the ways you can monitor it is to explore the differences in metrics as you tweak hyperparameters, such as embedding size, vocab size, etc.
- The sequence of words can be just as their existence. For example, the word good can have multiple meanings if it comes after the word not or very.
- 📖 **TensorFlow Datasets** are pre-packed datasets for practising various machine learning tasks. You can see information about all TensorFlow Datasets at the TensorFlow datasets GitHub page: [https://github.com/tensorflow/datasets/](https://github.com/tensorflow/datasets/)
    - See a full list of the datasets here: [https://www.tensorflow.org/datasets/catalog/overview](https://www.tensorflow.org/datasets/catalog/overview)
- Example code of loading the IMDB subwords dataset (IMDB dataset with subwords embeddings):

```python
import tensorflow_datasets as tfds
imdb, info = tfds.load("imdb_reviews/subwords8k",
											 with_info=True,
											 as_supervised=True)

# Accessing the data
train_data, test_data = imdb["train"], imdb["test"]

# Getting the subwords encoder/tokenizer
tokenizer = info.features['text'].encoder

# Check the subwords
print(tokenizer.subwords)

# Check to see how the tokenizer encodes or decodes strings
sample_string = 'TensorFlow, from basics to mastery'

# Encode the string
tokenized_string = tokenizer.encode(sample_string)
print('Tokenized string is {}'.format(tokenized_string))

# Decode the string
original_string = tokenizer.decode(tokenized_string)
print('The original string: {}'.format(original_string))

```

- Subwords embeddings don't work great with dense networks (it's very hard to pull meaning out of singular pieces of words). This is where you'll need to start using Recurrent Neural Networks, which deal far better with sequences.
- 📖 **Questions**
    - What is the name of the TensorFlow library containing common data that you can use to train and test neural networks?
        - TensorFlow Datasets.
    - How many reviews are there in the IMDB dataset and how are they split?
        - 50,000 records, 50/50 train/test split.
    - How are the labels for the IMDB dataset encoded?
        - Reviews encoded as a number 0-1.
    - What is the purpose of the embedding dimension?
        - It is the number of dimensions for the vector representing the word encoding.
    - When tokenizing a corpus, what does the num_words=n parameter do?
        - It specifies the maximum number of words to be tokenized and picks the most common 'n' words.
    - To use word embeddings in TensorFlow, in a sequential layer, what is the name of the class?
        - `tf.keras.layers.Embedding`
    - IMDB reviews are either positive or negative. What type of loss function should be used in this scenario?
        - Binary crossentropy.
    - When using IMDB Sub Words dataset, our results in classification were poor. Why?
        - Sequence becomes much more important when dealing with subwords, because we're ignoring word positions.
            - E.g. Tensor broken into "Ten" and "sor" could have multiple meanings. "Ten" could mean the number 10 on its own and something else when followed by "sor".

### Week 3 — Sequence models (LSTMs & Recurrent Neural Networks)

May 20, 2020

- Order matters in sequences of words. This is where you'll need a neural network model that can deal with sequences.
    - For example, "the dog sat on my hat" has different meaning to "sat hat on my the dog"
- For an in-depth look at sequence models, check out this series of lectures by Andrew Ng:

[Sequence Models (Course 5 of the Deep Learning Specialization) - YouTube](https://www.youtube.com/playlist?list=PLkDaE6sCZn6F6wUI9tvS_Gw1vaFAx6rd6)

- For a sequence model, imagine each neuron not only does it produce an output from an input and passes it to another neuron, it also passes the things it thought about that output to the next neuron. This passing of intermediate thoughts is often referred to as a the hidden state.

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-20_at_9.50.05_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-20_at_9.50.05_am.png]]

Inputs (X) are passed to F then outputted as y, F also passes the patterns its learned to F+1. Image from TF in Practice on Coursera.

- LSTMs have another parameter called the cell state which helps keep the context from earlier tokens in relevance to later ones, thus helping with longer sequences.
    - The cell-state can also be bidirectional (this is known as a bidirectional RNN).

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-20_at_9.54.42_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-20_at_9.54.42_am.png]]

Example of a bidirectional cell state (flows left and right) across a series of RNN cells. The cell state helps keep information across a range of cells, for example, the information from X0 to influence X2 and vice versa. Image from TF in Practice on Coursera.

- If you want to stack LSTMs in a model, you need to add the `return_sequences=True` parameter. This ensures the outputs of the first LSTM cell match the inputs of the second LSTM cell.

```python
# Example of stacking LSTM cells in a model
model = tf.keras.Sequential([
	tf.keras.layers.Embedding(tokenizer.vocab_size, 64),
	# Bidirectional layer which will return its outputs ready for the next layer
	tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(64, return_sequences=True)),
	tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32)),
	tf.keras.layers.Dense(64, activation='relu'),
	tf.keras.layers.Dense(1, activation='sigmoid')])
```

- Be careful when you're getting sharp dips in your training curves, it means your models may need to  be improved.
- Example of using a Convolutional 1D model with filter size 5 (meaning it groups together 5 words at a time):

```python
model = tf.keras.Sequential([
	tf.keras.layers.Embedding(vocab_size,
														embedding_dim,
														input_length=max_length),
	# Group together words in sequences of size 5
	tf.keras.layers.Conv1D(128, 5, activation='relu'),
	tf.keras.layers.GlobalMaxPooling1D(),
	tf.keras.layers.Dense(24, activation='relu'),
	tf.keras.layers.Dense(24, activation='relu'),
	tf.keras.layers.Dense(1, activation='sigmoid')])
```

- 🔑 Overfitting often occurs in text datasets due to the fact you've got text and words in the validation/testing vocabulary that you don't have in the training vocabulary.
    - E.g. you'll have plenty of oov_token = "<OOV>" words in the valid/test sets which can't be classified thus leading to higher loss values.
- 📖 **Questions**
    - Why does sequence make a large difference when determining the semantics of language?
        - Because the order in which words appear dictate their impact on the meaning of the sentence.
    - How do Recurrent Neural Networks help you understand the impact of sequence on meaning?
        - They carry meaning from one cell to the next.
    - How does an LSTM help understand meaning when words that qualify each other aren't necessarily beside each other in a sentence?
        - Values from earlier words can be carried to later ones via a cell state. (this cell state can be bidirectional)
    - What Keras layer type allows LSTMs to look forward and backward in a sentence?
        - `tf.keras.layers.Bidirectional(INSERT_CELL_TYPE_HERE)`
    - What's the output shape of a bidirectional LSTM layer with 64 units?
        - (None, 128) — 64*2 since it's bidirectional
    - When stacking LSTMs, how do you instruct an LSTM to feed the next one in the sequence?
        - Ensure that `return_sequences=True` only on units that feed to another LSTM.
    - If a sentence has 120 tokens in it, and a Conv1D with 128 filters with a Kernel size of 5 is passed over it, what's the output shape?
        - (None, 116, 128) — [batch, length (minus padding), num_filters]
    - What's the best way to avoid overfitting in NLP datasets?
        - No cell type (LSTM, GRU) or layer type (Conv1D) is immune to overfitting. Solving overfitting usually takes some practice with manipulating the model type and making sure your data splits are ideal for the problem you're working on.

### Week 4 — Sequence models and literature

May 21, 2020

- Text generation is a prediction problem. Get a body of text, create a training dataset with the sequences where the X's are the first few words and the y's (labels) are the next few words.
    - E.g. given a sample of words, predict what words should come after
- Example of finding the max length in a sequence:

```python
max_sequence_len = max([len(x) for x in list_of_sequences])
```

- Example of one-hot encoding a series of labels:

```python
ys = tf.keras.utils.to_categorical(labels, num_classes=total_words)
```

- Tokenizing a string of words:

```python
tokenizer = Tokenizer()

data= 'some string of words'

# Lower and split on newlines (if needed)
corpus = data.lower().split('\n')

# Fit the tokenizer on the texts
tokenizer.fit_on_texts(corpus)

# Number of words in the vocabulary
total_words = len(tokenizer.word_index) + 1
```

- Example of setting up a simple sequential model to generate text:

```python
model = Sequential()
model.add(Embedding(total_words,
										64,
										input_length=max_sequence_len - 1))
model.add(Bidirectional(LSTM(20))) # set the LSTM to go back and forth
model.add(Dense(total_words, activation='softmax'))
model.compile(loss='categorical_crossentropy',
							optimizer='adam',
							metrics=['accuracy'])
model.fit(xs, ys, epochs=500, verbose=1)
```

- Link to Laurence's preprocessed poetry dataset for generating text: [https://storage.googleapis.com/laurencemoroney-blog.appspot.com/irish-lyrics-eof.txt](https://storage.googleapis.com/laurencemoroney-blog.appspot.com/irish-lyrics-eof.txt)
    - This link contains 1600+ sentences of Irish songs and poetry.
- 🔑 3 things you can try to experiment with sequence models:
    1. The dimension of the embedding
    2. The number of units in the LSTM
    3. The optimizer and learning rate
    4. Bonus: Try adjusting the number of epochs, remember training for longer will usually help but eventually you'll hit the law of diminishing returns (an early stopping callback can help you here).
- Went through the TensorFlow tutorial on building a character-based RNN: [https://www.tensorflow.org/tutorials/sequences/text_generation](https://www.tensorflow.org/tutorials/sequences/text_generation)
    - Character-based RNN meaning the RNN is trained to predict the next character in a sequence rather than the next word.
- 📖 **Questions**
    - What is the name of the method used to tokenize a list of sentences?
        - `fit_on_texts(sentences)`
    - If a sentence has 120 tokens in it, and a Conv1D with 128 filters with a Kernel size of 5 is passed over it, what's the output shape?
        - (None, 116, 128)
    - What is the purpose of the embedding dimension?
        - It is the number of dimensions for the vector representing the word encoding.
    - IMDB reviews are either positive or negaitve. What type of loss function should be used in this scenario?
        - Binary crossentropy.
    - If you have a number of sequences of different lengths, how do you ensure that they are understood when fed into a neural network?
        - Use the `pad_sequences` object from the `tensorflow.keras.preprocessing.sequence` namespace.
    - When predicting words to generate poetry, the more words predicted the more likely it will end up gibberish, why?
        - Because the probability that each word matches an existing phrase goes down the more words you create.
    - What is a major drawback of word-based training for text generation instead of character-based generation?
        - Memory constraints: because there are far more words in a typical corpus than characters, it is much more memory intensive.
    - How does an LSTM help understand meaning when words that qualify each other aren't necessarily beside each other in a sentence?
        - Values from earlier words can be carried to later ones via a cell state.

---

## Part 2 — Computer vision with TensorFlow

### Week 1 — Exploring a Larger Dataset

May 13, 2020

- 🔑 **Data augmentation** (flipping and rotating images) adds the ability to prevent overfitting.
- In reality, downloading data from the internet involves a lot of data cleaning. Before you can run a model on a dataset, you'll need to clean it and prepare it in a way it can be used with your code.
- **Overfitting** is one of the central problems in machine learning. If your model is overfitting the training set, it means it won't generalize well to unseen data.
- 🔑 You can use the Keras `model.layers` API to find the outputs of each layer and iterate through them to create a visualization model for each one.
- When you call `model.fit()` , you can save the outputs to a `history` variable. You can then use this variable for later inspection and plotting.

```python
# Save model.fit() to history and plotting results

# Fit the model
history = model.fit(train_dataflow,
          epochs=15,
          validation_data=valid_dataflow,
          steps_per_epoch=100,
          validation_steps=50,
          callbacks=[callbacks])

## Plot the history of our model

# Get the different results
acc = history.history["accuracy"]
val_acc = history.history["val_accuracy"]
loss = history.history["loss"]
val_loss = history.history["val_loss"]

epochs = range(len(acc))

# Plot the training and validation accuracy per epoch
plt.plot(epochs, acc)
plt.plot(epochs, val_acc)
plt.title("Training and validation accuracy")
plt.figure()

# Plot the training and validation loss per epoch
plt.plot(epochs, loss)
plt.plot(epochs, val_loss)
plt.title("Training and validation loss")
plt.figure()
```

- 📖 **Questions**
    - What does `flow_from_directory()` give you?
        - The ability to easily load images, to be able to pick the size of images, to automatically label images based on their directory name.
    - If my image is sized 150x150 and I pass a 3x3 convolution over it, what size is the resulting image?
        - 148x148
    - If my data is is sized 75x75 and I use Pooling of size 2x2, what size will the resulting image be?
        - 75x75 (halved)
    - If you want to view the history of training, how can you access it?
        - Create a `history` variable and assign it to the return of `model.fit()`
    - What's the name of the API that allows you to inspect the impact of convolutions on the images?
        - The model.layers API
    - When checking the result graphs, the loss levelled out at about .75 after 2 epochs, but the accuracy climbed close to 1.0 after 15 epochs, what's the significance of this?
        - There was no point training after 2 epochs, as we overfit the training data (you want the loss to keep going down).
    - Why is the validation accuracy a better indicator of model performance than training accuracy?
        - The validation accuracy is based on images that the model hasn't been trained with, and thus a better indicator of how the model will perform with new images.
    - Why is overfitting more likely to occur on smaller datasets?
        - Because there's less likelihood of all possible features being encountered in the training process.

### Week 2 — Data augmentation

May 14, 2020

- 🔑 **Image augmentation** involves manipulating an image to increase the size of your dataset and help reduce the overfitting of your model. For example, if you have 1000 images you could flip those images on the vertical axis and effectively increase your dataset size to 2000. There are other techniques you can do such as:
    - Flipping
    - Rotating
    - Cropping
    - Skewing
- The best way to do image augmentation is to manipulate it in memory.
- One of the interesting things about data augmentation is that it's not widely documented.
- If you've only seen one type of shoe in your life (boots) and you're shown another photo of a boot you'll recognize it. But if you're shown a picture of a high heel, you probably won't recognize it as a shoe.
- 📖 Different image preprocessing steps in Keras: [https://keras.io/api/preprocessing/image/](https://keras.io/api/preprocessing/image/)
- 🔑 **Steps per epoch** = divide number of training samples by batch size.
    - e.g. `steps_per_epoch = len(train) / batch_size`
- Example code for doing image augmentation:

```python
# ImageDataGenerator for doing image augmentation
train_datagen = ImageDataGenerator(
	rescale=1./255,
	rotation_range=40, # rotate image
	width_shift_range=0.2, # move image left or right
	height_shift_range=0.2, # move image up or down
	shear_range=0.2, # skew image
	zoom_range=0.2, # zoom in on image
	horizontal_flip=True, # flip image on horizontal
	fill_mode='nearest')

# See Keras's documentation for more: https://keras.io/api/preprocessing/image/
```

- 🔑 Without image augmentation, your model could be prone to overfitting. Some steps you might want to take:
    - Try and overfit a model first
    - See if image augmentation reduces overfitting
    - If overfitting continues, add dropout for further regularization
- Keep in mind, you need a broad set of images for training as well as a broad set of images for testing. If data augmentation changes your images too much, you might notice the performance on your validation set not keeping up (this is because the validation set doesn't contain the same style of augmented images from the training set).
- 📖 **Questions**
    - How do you use Image Augmentation in TensorFlow?
        - By passing parameters to the `ImageDataGenerator`.
    - If your training data only has people facing left, but you want to classify people facing right, how could you prevent overfitting?
        - Use the `horizontal_flip` parameter passed to `ImageDataGenerator`
    - Why is training with augmentation slower?
        - Because the image processing (flipping, shifting, cropping images) takes cycles to complete.
    - What does the `fill_mode` parameter of `ImageDataGenerator` do?
        - It attempts to recreate lost pixels after a transformation like a shear.
    - When using Image Augmentation with the `ImageDataGenerator`, what happens to your raw image data on disk?
        - Nothing, all augmentation is done in-memory.
    - How does Image Augmentation help solve overfitting?
        - It manipulates the training set to generate more scenarios for features in the images. Effectively increasing the size of your training set.
    - When using Image Augmentation my training gets...
        - Slower. But is more robust to overfitting.
    - Using Image Augmentation effectively simulates having a larger data set for training. True or False?
        - True.

**Next:**

- [x]  Programming exercise: Cats vs. Dogs using augmentation
- 🔑 Example code for uploading a single image into Google Colab and using as the target for predicting:

```python
# This code will upload an image to Google Colab and make a prediction on it with a trained model
import numpy as np
from google.colab import files
from keras.preprocessing import image

uploaded = files.upload()

for fn in uploaded.keys():

  # predicting images
  path = '/content/' + fn
  img = image.load_img(path, target_size=(# YOUR CODE HERE))
  x = image.img_to_array(img)
  x = np.expand_dims(x, axis=0)

  images = np.vstack([x])
  classes = model.predict(images, batch_size=10)
  print(classes[0])
  if classes[0]>0.5:
    print(fn + " is a dog")
  else:
    print(fn + " is a cat")
```

### Week 3 — Transfer Learning

May 15, 2020

- 🔑 **Transfer learning** allows you to leverage the features and patterns another model has learned in your own model. You can also slightly retrain an existing model and apply it to your own task.
- 📖 Example of transfer learning workflow using TensorFlow: [https://www.tensorflow.org/tutorials/images/transfer_learning](https://www.tensorflow.org/tutorials/images/transfer_learning)
- When downloading a pretrained model such as Inception V3, it's common to want to only get the underlying layers and ignore the top layer (usually a dense layer), you can do this by setting the parameter `include_top` to False.

```python
from tensorflow.keras.applications.inception_v3 import InceptionV3

local_weights_file = '/tmp/inception_v3_weights_tf_dim_ordering_tf_kernels_notop.h5'

pretrained_model = InceptionV3(input_shape = (150, 150, 3),
															 include_top = False, # don't include the top layers
															 weights = None)

pre_trained_model.load_weights(local_weights_file)

```

- To make sure already pretrained layers aren't trained, you can set their `trainable` attribute to False:

```python
# Setting the trainable attribute of each layer to False
for layer in pre_trained_model.layers:
	layer.trainable = False # freeze or lock the underlying layers

# Check the summary of your model (be careful, it's huge)
pre_trained_model.summary()
```

- The following code grabs from Inception the layer called 'mixed7', which is the output from a lot of convolutions which are 7x7:

```python
last_layer = pre_trained_model.get_layer('mixed7')

last_output = last_layer.output # get the outputs
```

- We can then create our own DNN on top of the `last_output` layer which contains all of the patterns learned from the Inception model up to that layer.

```python
from tensorflow.keras.optimizers import RMSprop

# Take the last output layer and pass it through a DNN
x = layers.Flatten()(last_output)
x = layers.Dense(1024, activation='relu')(x)
x = layers.Dense(1, activation='sigmoid')(x)

model = Model(pre_trained_model.input, x)
model.compile(optimizer=RMSprop(lr=0.0001),
							loss='binary_crossentropy',
							metrics=['accuracy'])
```

- The above model overfits the training data, so one option is to add a dropout layer.

```python
# Add a dropout layer to prevent overfitting
x = layers.Flatten()(last_output)
x = layers.Dense(1024, activation='relu')(x)
x = layers.Dropout(0.2)(x) # add dropout with rate 0.2
x = layers.Dense(1, activation='sigmoid')(x)
```

- 📖 A great video explaining why dropout is helpful by Andrew Ng: [https://www.youtube.com/watch?v=ARq74QuavAo](https://www.youtube.com/watch?v=ARq74QuavAo)
- 🔑 **Dropout in a sentence**: remove some parts of your model randomly during training so the parts that remain get better at learning what's going on.
    - Like a company with 100 people, if the company depends too much on 1 person (1 neuron), chances of something going wrong for that company increase if the the problem doesn't concern the 1 person. Better to the let the rest of the company (the other neurons) learn how to handle certain situations, so if 1 person isn't available, the rest know what to do.
- 📖 **Questions**
    - If you use a dropout parameter of 0.2, how many nodes will you lose?
        - 20% of them.
    - Why is transfer learning useful?
        - Because I can use the features that were learned from large datasets that I may no have access to.
    - How do you lock of freeze a layer from retraining?
        - Set the layer's trainable attribute to False: `layer.trainable=False`
    - How do you change the number of classes the model can classify when using transfer learning? (e.g. the original model handled 1000 classes, but your handles just 2)
        - When you add your DNN at the bottom of the network, you specify your output layer with the number of classes you want. E.g. `tf.keras.layers.Dense(1, activation='sigmoid')` for binary classification.
    - Can you use Image Augmentation with Transfer Learning Models?
        - Yes, because you are adding new layers at the bottom of the network, and you can use image augmentation when training these.
    - Why do dropouts help avoid overfitting?
        - Because neighbouring neurons can have similar weights, and thus can skew the final training.
    - What would the symptom of a Dropout rate being set too high?
        - The network would lose specialization down the effect that it would be inefficient or ineffective at learning, driving accuracy down.
    - How would you add a dropout layer to dropout 20% of neurons using TensorFlow?
        - `tf.keras.layers.Dropout(0.2)`
- 🚫 Noticing the average viewership of different learning materials reduces with each major section, e.g. Week 1, part 1 had 10,000+ but Week 3, part 2 has ~2,000. Meaning, people either use the free-trial then dropout or the longer you commit, the more knowledge you'll gain over others.
- 🚫 Grader failed on the programming assignment again, don't really care (the code matters more), moving onto the next module.

**Next:**

- [ ]  Multiclass classifications: [https://www.coursera.org/learn/convolutional-neural-networks-tensorflow/home/week/4](https://www.coursera.org/learn/convolutional-neural-networks-tensorflow/home/week/4)

### Week 4 — Multiclass classifications

May 15, 2020

- 🔑 A **mutliclass classifier** classifies an instance into one of multiple categories. For example, taking a photo of a letter of the alphabet and classifying what letter it is.
- For multiple classes of data, you'll have to change your data generator's `class_mode` to `'categorical'` :

```python
train_datagen = ImageDataGenerator(rescale=1./255)

train_datagenerator = train_datagen.flow_from_directory(train_dir,
																												target_size=(300, 300),
																												batch_size=128,
																												# this changes
																												class_mode='categorical')

```

- You also have to change your output layer to have an activation function of `'softmax'`:

```python
# The output layer has to have the same number of neurons
# as you have number of classes. Also activation changes to softmax.
tf.keras.layers.Dense(num_classes, activation='softmax')
```

- Finally, you have to change your model compiler, the loss function changes to `'categorical_crossentropy'`:

```python
model.compile(loss='categorical_crossentropy',
							optimizer=Adam(),
							metrics=['accuracy'])
```

- 📖 **Questions**
    - Why does the DNN for Fashion MNIST have 10 output neurons?
        - Because the dataset has 10 classes (10 different pieces of fashion items).
    - What is a convolution?
        - A technique to extract features from an image.
    - Applying convolutions on top of a DNN will have what impact on training?
        - It depends on many factors. It might make your training faster or slower, and a poorly designed convolutional layer may even be less efficient than a plain DNN!
    - What method within an ImageGenerator is used to normalize the image?
        - `rescale` — example: `train_datagen = ImageDataGenerator(rescale=1./255)`
    - When using Image Augmentation with the ImageDataGenerator, what happens to your raw image data on-disk?
        - Nothing. All augmentation happens in memory.
    - Can you use Image Augmentation with Transfer Learning?
        - Yes. The pre-trained layers of a previously trained model get frozen. So you can augment your images as you train the bottom layers of the DNN with them.
    - When training for multiple classes what is the Class Mode for Image Augmentation?
        - `class_mode='categorical'`
- Example of adding an extra axis to NumPy arrays:

```python
# In this section you will have to add another dimension to the data
# So, for example, if your array is (10000, 28, 28)
# You will need to make it (10000, 28, 28, 1)
# Hint: np.expand_dims

# Change shape to add an extra axis
training_images = training_images[:, :, :, np.newaxis]
testing_images = testing_images[:, :, :, np.newaxis]
```

---

## Part 1 — Introduction to TensorFlow for Artificial Intelligence, Machine Learning and Deep Learning

### Week 1 — A primer in machine learning

May 11, 2020

- Rules schmules. Let the computer figure them out.
- Be aware of two functions:
    - Optimizers — how a model should improve its guesses
    - Loss — how wrong a model's guesses are

🚫 The assignment submission isn't working... doesn't really matter. Made a code solution to go along with it.

```python
"""
Make a function which trains a neural network to predict
house prices following the rule:
price = $50k + $50k * number of bedrooms
"""
def house_model(y_new):
	  # Number of bedrooms
    xs = np.array([10.0, 5.0, 6.0, 8.0, 4.0, 3.0, 9.0, 5.0, 2.0, 1.0, 50.0], dtype=float)
		# Price (in hundreds of thousands)
    ys = np.array([5.5, 3.0, 3.5, 4.5, 2.5, 2.0, 5.0, 3.0, 1.5, 1.0, 25.5], dtype=float)
    model = tf.keras.Sequential([keras.layers.Dense(units=1, input_shape=[1])])
    model.compile(optimizer="adam",
									loss="mean_squared_error")
    model.fit(xs, ys, epochs=100)
    return model.predict(y_new)[0]

print(house_model([7])) # should come close to 4
```

### Week 2 — Introduction to Computer Vision

May 11, 2020

- Computer vision is teaching a computer to figure out what's in an image.
- Fashion MNIST is a toy dataset for computer vision — [https://github.com/zalandoresearch/fashion-mnist](https://github.com/zalandoresearch/fashion-mnist)
    - 10 categories
    - 70k images
    - Images are 28x28 pixels in greyscale (1-dimension)
- Labelling data with numbers prevents bias to different languages
    - e.g. Ankle boot could be labelled with "9" that way people from other non-English languages can recognize the classname
- 🔑 Training a neural network it's better to have your values between 0 & 1 (e.g. pixel values), this process is called "**normalizing**".
    - Without doing so, your network could take longer to learn.

```python
# Normalize pixel values by dividing them by 255.0 (if they're between 0 to 255)
training_images = training_images / 255.0
test_images = test_images / 255.0
```

- 📖 **Definitions to note**
    - **Sequential:** Defining a sequence of layers in a neural network.
    - **Flatten:** Convert an array shape into a 1-dimensional set.
    - **Dense:** A layer of neurons of a certain size.
    - **Activation function:** Tells a neuron what to do.
    - **Relu activation:** (Rectified Linear Unit) Says if X is greater than 0 return X, if not return 0. In essence only values greater than 0 move through the network.
    - **Softmax activation:** Picks the biggest value from a set of values and returns 1 for that value and 0 for the rest. For example, [0.03, 0.94, 0.02, 0.01] would turn into [0, 1, 0, 0].
- 🔑 The number of neurons in the last layer should match the number of target classes you have. If you're trying to classify 10 different classes of food, your final layer should have 10 neurons.
- 🚫 One of the most common errors you'll run into is shape mismatches. For example, if your outputs are meant to be 10 classes, but your final layer only has 5 neurons.
- 🔑 If your labels are some kind of integer, for example, [0, 1, 2, 3], use `sparse_categorical_crossentropy`, if they're one-hot encoded, use `categorical_crossentropy`.

```python
# Computer vision model in one cell
import tensorflow as tf

# Setup data
mnist = tf.keras.datasets.fashion_mnist

# Split data into train and test
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

# Normalize images
train_images = train_images / 255.0
test_images = test_images / 255.0

# Create a model
model = tf.keras.Sequential([tf.keras.layers.Flatten(),
														 tf.keras.layers.Dense(128, activation="relu"),
														 tf.keras.layers.Dense(10, activation="softmax")])

# Compile the model
model.compile(optimizer="adam",
							loss="sparse_categorical_crossentropy",
							metrics=["accuracy"])

# Fit the model
model.fit(train_images, train_labels, epochs=5)

# Evaluate the model
model.evaluate(test_images, test_labels)
```

- 📖**Callbacks** can be used to control different parts of training, such as, stopping a model once it reaches a certain level of accuracy.

```python
# Example of implementing a callback with TensorFlow
import tensorflow as tf

# This callback class stops the model training once it hits 60% accuracy
class myCallback(tf.keras.callbacks.Callback):
	# It needs to be called this "on_epoch_end" to happen at the end of an epoch
	def on_epoch_end(self, epoch, logs={}):
		if(logs.get("accuracy")>0.6):
			print("\nReached 60% accuracy so cancelling training!")
			self.model.stop_training = True

callbacks = myCallback()

# THIS IS THE FASION MNIST, LOAD IT
mnist = tf.keras.datasets.fashion_mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
train_images, test_images = train_images / 255.0, test_images / 255.0

model = tf.keras.models.Sequential([tf.keras.layers.Flatten(input_shape=(28, 28)),
														 tf.keras.layers.Dense(128, activation="relu"),
														 tf.keras.layers.Dense(10, activation="softmax")])

model.compile(loss="sparse_categorical_crossentropy",
							optimizer="adam",
							metrics=["accuracy"])

# The model will stop training when it hits 60%+ accuracy
model.fit(train_images, train_labels, epochs=5, callbacks=[callbacks])
```

- 🚫 Again my assignment didn't pass the tests... although it worked in practice. (maybe because we used "spare" instead of "sparse"?)

```python
# This code/model should achieve 99%+ on MNIST after around 6 epochs
def train_mnist():
    class myCallback(tf.keras.callbacks.Callback):
        def on_epoch_end(self, epoch, logs={}):
            if (logs.get("acc")>0.99):
                print("Reached 99% accuracy so cancelling training!")
                self.model.stop_training = True

    callbacks = myCallback()

		# You need to load MNIST (DIGITS ONE)
    mnist = tf.keras.datasets.mnist
    (x_train, y_train),(x_test, y_test) = mnist.load_data(path=path)
    x_train = x_train / 255.0
    x_test = x_test / 255.0
    model = tf.keras.models.Sequential([
        tf.keras.layers.Flatten(input_shape=(28, 28)),
        tf.keras.layers.Dense(256, activation="relu"),
        tf.keras.layers.Dense(128, activation="relu"),
        tf.keras.layers.Dense(10, activation="softmax")
    ])

    model.compile(optimizer='adam',
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])

    # model fitting
    history = model.fit(
        x_train,
        y_train,
        epochs=10,
        callbacks=[callbacks]
    )
    # model fitting
    return history.epoch, history.history['acc'][-1]

train_mnist()
```

### Week 3 — Enhancing Vision with Convolutional Neural Networks

May 11, 2020

- Example of a vertical convolutional filter:

[[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-11_at_9.42.24_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-11_at_9.42.24_am.png]]

- 📖If you want an in-depth guide on convolutions, check out the following YouTube playlist:

[Convolutional Neural Networks (Course 4 of the Deep Learning Specialization) - YouTube](https://www.youtube.com/playlist?list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF)

- Example of a convolutional model in Keras (the Conv2D and MaxPooling2D layers are explained in the above YouTube playlist):

```python
model = tf.keras.models.Sequential([
	tf.keras.layers.Conv2D(64, (3, 3), activation='relu',
												 input_shape=(28, 28, 1)) # height, width, channels
	tf.keras.layers.MaxPooling2D(2, 2),
	tf.keras.layers.Conv2D(64, (3, 3), activation='relu'),
	tf.keras.layers.MaxPooling2D(2, 2),
	tf.keras.layers.Flatten(),
	tf.keras.layers.Dense(128, activation='relu'),
	tf.keras.layers.Dense(10, activation='softmax')
])

# Get the summary of the model
model.summary()
```

- Depending on the size of your filter, the output shape (shown in `model.summary()` ) may be reduced compared to your original input shapes.
    - Max pooling also reduces the size of your shape (condensing the details to make them more manageable).
- 🔑 **Convolutional layers and max pooling in a nutshell:** find the major features of an image and condense them down to be representative of that image, this condensation of information makes it easier for a neural network to learn it.
- 📖 Different convolutional filters have different effects on an image. For example, there's a horizontal filter, a vertical filter and more: [https://lodev.org/cgtutor/filtering.html](https://lodev.org/cgtutor/filtering.html)
- 📖 **Questions on convolutions**
    - What is a convolution?
        - A technique to isolate features in images.
    - What is a pooling?
        - A technique to reduce the information in an image while maintaining features.
    - How do convolutions improve image recognition?
        - They isolate features in images.
    - After passing a 3x3 filter over a 28x28 image, how big will the output be?
        - 26x26 (you lose 2 pixels from the height and width to make room for the filter)
    - After max pooling a 26x26 image with a 2x2 filter, how big will the output be?
        - 13x13 (half the image size)
    - What will applying convolutions on top of our deep neural network do to training?
        - It depends. It may make training faster or slower. Usually it'd make it slower. Be careful though, a poorly designed convolutional layer may even make your models predictions worse.

### Week 4 — Using real-world images

May 12, 2020

- Inspiring video on how TensorFlow can be used to solve problems around the world, such as, detecting diseases on crops:

[https://www.youtube.com/watch?v=NlpS-DhayQA](https://www.youtube.com/watch?v=NlpS-DhayQA)

- ImageGenerator is a Keras API which can help to create labels out of a directory. If images are within a certain directory, they can be labelled based on the names of that directory.

    [[%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-12_at_9.30.07_am.png|%5BCourse%5D TensorFlow in Practice on Coursera Notes/Screen_Shot_2020-05-12_at_9.30.07_am.png]]

- Example of using the ImageDataGenerator

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# Normalize the pixels
train_datagen = ImageDataGenerator(rescale=1./255)

# Make the images flow in from the training directory (resizing as they go)
train_datagenerator = train_datagen.flow_from_directory(train_dir,
	target_size=(300, 300), # make sure all images are the same size
	batch_size=128, # how big are the batches? 32, 64, 128 are usually good numbers
	class_mode='binary') # binary classification

```

- 🔑 For binary classification, use a `'sigmoid'` activation.
    - Also, use `'binary_crossentropy'` as the loss function in `model.compile()`
- 🚫 When using image generators, you don't fit models using a regular `fit()` function, you use a `fit_generator()` function.
    - **Note**: `fit_generator()` will be deprecated soon, `fit()` will support generators from now on.
- 📖 Information on different loss metrics is available in Google's Machine Learning Crash Course: [https://developers.google.com/machine-learning/crash-course/descending-into-ml/video-lecture](https://developers.google.com/machine-learning/crash-course/descending-into-ml/video-lecture)
- Optimizers like RMSProp, Adam and Adagrad all adaptively change the learning rate.
    - It's important to adjust the learning rate as a model learns more, too big and the gradients could explode, too small and the gradients could vanish.
- Example of uploading a file into Google Colab and making a prediction on it:

```python
import numpy as np
from google.colab import files
from keras.preprocessing import image

uploaded = files.upload()

for fn in uploaded.keys():

  # predicting images
  path = '/content/' + fn
  img = image.load_img(path, target_size=(300, 300))
  x = image.img_to_array(img)
  x = np.expand_dims(x, axis=0)

  images = np.vstack([x])
  classes = model.predict(images, batch_size=10)
  print(classes[0])
  if classes[0]>0.5:
    print(fn + " is a human")
  else:
    print(fn + " is a horse")
```

- The deeper you get in a neural network, the more sparse the feature representations the model learns. The model ends up being a compressed form of the data.
- You can change the input size of your images to the `input_shape` parameter of your input layer, however, this might influence your models performance (it may go faster, but it may end up with worse results).
- 📖 **Questions**
    - Using Image Generator, how do you label images?
        - Images are labelled based on the name of the directory they are contained in.
    - What method on the Image Generator is used to normalize the image?
        - `rescale` — e.g. `train_datagen = ImageGenerator(rescale=1./255)`
    - How do you specify the training size for the images?
        - Using the `target_size` parameter on the training generator.
        - e.g.

        ```python
        train_generator = train_datagen.flow_from_directory(
        	dir_name="target_dir",
        	target_size=(300, 300),
        	batch_size=32,
        	class_mode="binary")
        ```

    - What does `input_shape = (300, 300, 3)` mean?
        - Images are 300x300 pixels with 3 colour channels.
    - If your training data is close to 1.000 accuracy, but your validation data isn't, what's the risk here?
        - You're overfitting on the training data (too high of results).
    - Convolutional neural networks are better for classifying images like horses and humans because:
        - There are a wide variety of humans and horses all with similar but differing features.
    - After reducing the size of the images, the training results were different, why?
        - We removed some convolutions to handle the smaller image (when using smaller images, less convolutional layers may have to be used because otherwise the information will be too compressed).
