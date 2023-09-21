---
share: "true"
---
> [!note] These notes are not mine. 
# [Book] Hands-on Machine Learning with Scikit-Learn, Keras & TensorFlow Notes

All book notes from the [Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow by Aurélien Géron (2nd edition)](https://amzn.to/3aYexF2) for general machine learning study as well as [preparation for the TensorFlow Developer Certification](https://www.notion.so/Getting-TensorFlow-Developer-Certified-Curriculum-ff8385b6f9284fdfbc930ea06ce8749c).

**Game plan:** Read it cover to cover. No in-depth note-taking, only notes on topics and pages I'd like to revisit for the second pass. Come back and revisit after reading through.

## To do

- [ ]  Read the book cover to cover — 799 pages means about 30 pages per day minimum to do it in a month
    - [ ]  Take notes on topics and pages to revisit
- [ ]  Go back through the book, revisiting topics and different pages from above
    - [ ]  Take more in-depth notes and create practical examples

## Resources

- Book on Amazon: [https://amzn.to/3aYexF2](https://amzn.to/3aYexF2) (I have the digital version on Moon Reader)
- Code examples to go along with the book (use the google collab. Mac with i9 9th gen overheats): [https://github.com/ageron/handson-ml2](https://github.com/ageron/handson-ml2)

## Key

- 🔑 = Major key, something to remember and come back to
- 📖 = Extra resource or reading
- 🚫 = Error/issue

## Notes

**Chapter 1: The Machine Learning Landscape**

- TensorFlow: a complex library for distributed numerical computation.
- 5 — what machine learning is great for
- 6 — examples of machine learning projects and problems
- 9 — most important supervised learning algorithms
- 10 — most important unsupervised learning algorithms
- 15 — difference between batch learning and online learning
- 16 — learning rate and new data
- 23 — two things which can go wrong: bad algorithm, bad data
- 27 — feature engineering overview
- 28 — regularization (reducing the risk of overfitting)
- 31 — validation set (held out for optimizing hyperparameters)
- 33 — no free lunch theorem (different models for different tasks)

**Chapter 2: End-to-End Machine Learning Project**

- 36 — lists of places to get real world data (open source data sources)
- 38 — machine learning pipelines
- 40 — common machine learning notations
- 41 — RSME + MAE & L1 + L2 norms (RMSE = L2, MAE = L1)
- 42 — creating a workspace environment
- 46 — creating a function to download data
- 49 — bell-curve standard deviation rules
- 53 — creating randomized and reproducible data splits

<aside>
💡 55 — While splitting the dataset, instead of totally random splits, categorized/Stratified shuffle splitting created test and train sets that represent the overall data more closely.

</aside>

- 56 — setting an alpha property makes it easier to Visualize where there is a high density of points
- 59 — correlation matrix, positive + negative correlation
- 60 — pandas scatter_matrix()
- 63 — sklearn SimpleImputer
- 64 — sklearn design, estimators, predictors (fit(), fit_transform(), etc)
- 67 — OneHotEncoder, sparse matrix versus NumPy array
- 68 — creating a custom data transformation class in sklearn
- 75 — “the goal is to shortlist 2-5 promising models
- 78 — when the hyperparameter space is large, it is often preferred to use RandomizedSearchCV instead of GridSearchCV (saves time)
- 78 — feature importance
- 80 — using `scipy.stats.t.interval()` to calculate the 95% confidence interval
- 81 — overview of deploying a model to Google Cloud AI Platform
- 92 — precision and recall examples
- 95 — plotting a precision versus recall curve to figure out the ideal cutoff threshold
- 98 — ROC or PR (precision & recall) curve
- 100 — mutliclass classification: one versus rest and one versus one classifiers
- 106 — multilabel classification

**Chapter 4: Training Models**

- 112 — linear regression
- 118 — gradient descent
- 123 — experiment with different learning rates
- 127 — minibatch gradient descent
- 128 — comparison of different optimisation algorithms (e.g. gradient descent vs mini batch gradient descent)
- 128 — polynomial regression
- 134 — the bias/variance trade off
- 135 — ridge regression, lasso regression and elastic net: 3 ways of regularizing (constraining the weights) lunar models
- 137 — lasso regression is like ridge regression (adds a regularisation function) but uses l1 norm instead of l2 norm
- 140 — 💡when should you use Linear Regression, Lasso, Ridge or Elastic regression?
- 141 — early stopping: the beautiful free lunch (a great regularisation technique)
- 142 — logistic regression
- 147 — regularisation prevents overfitting, `C` is `LogisticRegression`’s regularisation parameter, the higher `C`, the more regularised the model
- 148 — softmax regression (logistic regression but for multiple classes)

**Chapter 5: Support Vector Machines (SVMs) — SKIPPED**

**Chapter 6: Decision Trees**

- 176 — visualising decision trees
- 177 — decision trees are robust to feature scaling
- 181 — using Gini impurity or entropy as your decision trees cost function, which is better?
- 181 — how to regularise a decision tree (avoid overfitting)

**Chapter 7: Ensemble Learning and Random Forests**

- 192 — voting classifier (combination of other classifiers) performs better than any single classifier
- 197 — random forests
- 198 — extra tree classifiers are even more random than random forest classifiers, they train faster, however may underfit → best to train both and compare using cross-validation
- 208 — Use XGBoost as an optimized version of gradient boosting
- 💡212 — Good exercise to create an ensemble (stacking different classifiers together)

**Chapter 8: Dimensionality Reduction**

- 218 — manifold learning: a 2D object which can be represented with more dimensions
- 219 — Principle Component Analysis
- 223 — how to choose the right number of dimensions for your data
- 224 — PCA for compression (compressing images to less numbers of dimensions)
- 226 — Using Incremental PCA for large datasets

**Chapter 9: Unsupervised Learning Techniques**

- 235 — Yann LeCun: “If intelligence was a cake, unsupervised learning would be the cake, supervised learning would be the icing on the cake and reinforcement learning would be the cherry on the cake.”
- 236 — Clustering (grouping like examples together) is a great technique for semi-supervised learning.
- 245 — How to use KMeans/Clustering if your dataset does not fit in memory
- 245 — Finding the right number of clusters for KMeans
- 250 — KMeans clustering for image segmentation (segmenting colours)
- 252 — Reducing dimensionality with KMeans and improving error rates
- 255 — 💡Active learning: a common method is called uncertainty sampling.
    1. Model trained on the labelled instances gathered so far, and this model is used to make predictions on all the unlabelled instances.
    2. The instances for which the model is most uncertain (i.e., when its estimated probability is lowest) are given to the expert to be labelled.
    3. You iterate this process until the performance improvement stops being worth the labelling effort.
- 260 — Gaussian Mixture Models
- 264 — Probability density functions
- 266 — Anomaly detection using Gaussian Mixture Models
- 268 — Difference between probability and likelihood in statistics
- 272 — Bayes’ theorem
- 274 — Different approaches for anomaly detection, including PCA, Fast-MCD, Isolation Forest (anomaly detection with Random Forests and Decision Trees), Local Outlier Factor (LOF) and One-class SVM
- 275 — 🔨 Get hands-on with clustering and using KMeans for dimensionality reduction to bed fed into a classifier.

**Chapter 10: Introduction to Artificial Neural Networks with Keras**

- 290 — Automatic differentiation = automatically finding the gradients to reduce the error of a model
    - Backpropagation is done using the chain rule (perhaps the most fundamental rule in calculus)
- Sigmoid, hyperbolic tangent function (tanh()) and Rectified Linear Unit Function (ReLU)
    - ReLU has become the default because it is calculated faster
- 290 — Regression MLPs: you need one output neuron per output dimension
    - Different loss functions to use for regression: MSE by default but if you’ve got plenty of outliers use MAE. Or even Huber loss, a combination of both.
    - Structure of multi-layer perceptron
- 291 — Using MLPs for binary and multi class classification, classification architecture anatomy
- 296 — Two implementations of Keras, a stand-alone with multiple backends and `tf.keras` Which has all of TensorFlow’s features
- 298 — scaling the input features for gradient descent (gradient descent requires values between 0 & 1)
- 299 — creating a line-by-line neural network with Keras
- 300 — Using `model.summary()` or `Keras.utils.plot_model()` to view details of your models
- 302 — Compiling a keras model
- 303 — Tuning the learning rate with SGD using `optimizer=keras.optimizers.SGD(lr=???)`
- 305 — When plotting a training curve, shift it over half an epoch to the left
- 306 — Always retune the learning rate after changing any hyperparameter
- 307 — Creating a regression MLP using Keras Sequential API
- 308 — Use the functional Keras API for building more complex models
- 310 — Handling multiple inputs into the model
- 313 — Creating a model with the Keras Subclassing API (building dynamic models)
- 315 — You will typically use scripts to train, save and load models
    - You can also use callbacks to do various things whilst you model trains, such as saving checkpoints
- 316 — 💡How to create your own callbacks using `class callbackName(tf.keras.callbacks.Callback):`
- 317 — Using TensorBoard for visualisation
- 319 — Use `tf.summary` to create and write your own logs
- 320 — Fine-tuning neural network hyperparameters
    - You can wrap Keras’s models in a Scikit-Learn style fashion and then tune hyperparameters using GridSearchCV
- 322 — A range of different libraries for hyperparameter tuning such as, Hyperopt, Hyperas, Scikit-Optimize
- 324 — Different ways to optimize different hyperparameters such as, number of hidden layers, number of neurons per hidden layer, learning rate, batch size and more
- 326 — Tuning the learning rate:
    - "If you plot the loss as a function of the learning rate (using a log scale for the learning rate), you should see it dropping at first. But after a while, the learning rate will be too large, so the loss will shoot back up: the optimal learning rate will be a bit lower than the point at which the loss starts to climb (typically about 10 times lower than the turning point)."model.

**Chapter 11: Training Deep Neural Networks**

- 333 — Xavier or Glorot initialisation is used to prevent exploding or vanishing gradients (a special kind of random initialisation)
- 335 — Leaky ReLUs never die, they can go into a long coma, but they have a chance to eventually wake up
- 338 — Which activation function should you use? SELU > ELU > leaky ReLU > ReLU > tanh > logistic
- 341 — Using Batch Normalization as a regularisation technique
- 342 — Applying Batch Normalization with Keras
- 345 — Reusing pretrained layers (transfer learning)
- 347 — Transfer learning with Keras
- 348 — Freezing and unfreezing training layers in Keras
- 350 — Self-supervised learning
- 351 — Different optimizers other than gradient descent
- 353 — Setting momentum is one way to speed up gradient descent, a value of 0.9 typically works well in practice
    - Using `nesterov = True` is generally faster than pure momentum
- 356 — Adam optimizer, Adam = adaptive moment estimation
    - ▽𝑓 finds the direction of maximal change in f (For example, gradient descent, you want the direction of maximal change)
    - *Jacobian* = first order partial derivative, *Hessian* = second order partial derivative
- 359 — Optimizers compared by speed and quality
- 360 — Setting the learning rate & learning rate scheduling
    - Exponential decay, performance scheduling and 1cycle learning adjustments can considerably speed up convergence.
    - See the “learning rate scheduling” section of the notebook for an example.
- 365 — Dropout for regularisation
- 368 — Monte Carlo dropout for estimating model uncertainty

**Chapter 12: Custom Models and Training with TensorFlow**

- 377 — TensorFlow’s Python API

[[%5BBook%5D Hands-on Machine Learning with Scikit-Learn/image.jpg|%5BBook%5D Hands-on Machine Learning with Scikit-Learn/image.jpg]]

- 379 — Coding with TensorFlow and using it like NumPy
- 382 — Create a variable Tensor to make sure it can be updated (`tf.Variable([some_tensor])`)
- 383 — Different kinds of Tensors
- 384 — Creating a custom loss function
- 385 — Saving and loading models with custom components
- 387 — Custom activation functions, initialisers, regularisers and constraints
- 391 — Creating custom layers in Keras
    - 394 — What to do if your layer has different behaviours during training and testing
- 396 — Using the Sequential API, the Functional API and the Subclassing API you can build almost any model you find in a paper
- 397 — Building a custom Keras model with a custom loss function
- 399 — Using `tf.GradientTape()` to calculate gradients with Autodiff (automatic differentiation)
- 402 — Creating a custom training loop (replacing the `fit()` function), note: this should be avoided unless absolutely necessary, as it makes your code longer and more prone to errors
    - Creating a custom status printing metric
- 405 — Using TensorFlow Functions and Graphs
- 410 — Rules for creating TensorFlow functions

**Chapter 13: Loading and Preprocessing Data with TensorFlow**

- 413 — The TensorFlow Data API takes care of all the implementation details, such as multi threading, queuing, batching and prefetching for you.
    - 🔑 **Embedding:** A trainable dense vector that represents a category or token.
- 414 — The Data API revolves around the concept of a dataset: a sequence of data items
- 417 — Shuffling a dataset with a seed
- 419 — Preprocessing and scaling data with the Data API
- 420 — Example function putting together data preprocessing steps
- 423 — Using TensorFlow Datasets with Keras
    - 🔑 For CSV data, check out the `CsvDataset` class as well as the `make_csv_dataset()` method.
- 424 — Writing a custom training loop in Keras with a `@tf.function`
- 424 — 🔑 The TFRecord Format: TensorFlow’s preferred format for storing large amounts of data and reading it efficiently
- 426 — Using Protobufs with TFRecords
- 429 — Using `[tf.io](http://tf.io)` for images
    - Use the SequenceExample protobuf for working with sequence data
- 430 — Using `tf.RaggedTensor` to load sequence data which is of varying length
- 430 — Preprocessing data Input Features
    - Normalising features
    - Encoding categorical features
- 433 — Encoding Categorical Features Using Embeddings
- 434 — Word Embeddings: King - Man + Woman = Queen
- 435 — Making Embeddings manually
- 436 — Keras embedding layer for learning Embeddings
    - Other Keras preprocessing layers: [[httpsgithub.comkeras-teamgovernanceblobmasterrfcs20190502-preprocessing-layers.md]]
    - More available here: [https://keras.io/api/preprocessing/](https://keras.io/api/preprocessing/)
- 439 — Term Frequency x Inverse-Document-Frequency (TF-IDF)
- 440 — TensorFlow Extended (TFX) is an end-to-end platform for productionizing TensorFlow models
    - It lets you connect to Apache Beam for data processing amongst many other things
- 441 — TensorFlow Datasets (TFDS) project: downloading preformatted datasets ready to use
- 443 — 🔑 A great end-to-end text binary classification exercise for practice

**Chapter 14: Deep Computer Vision Using Convolutional Neural Networks**

- 448 — Convolutional layers
- 453 — Computing the output of a neuron in a Convolutional layer
    - TensorFlow implementation of Convolutional neural networks
- 455 — “SAME” padding versus “VALID” padding
- 456 — CNNs have a high memory requirement (because the reverse backward pass of backpropagation requires all the intermediate values computed during the forward pass)
    - If your training crashes because of out-of-memory issue, try the following:
        - Reduce the mini-batch size.
        - Reduce dimensionality with a stride or removing a few layers.
        - Try 16-bit floats instead of 32-bit floats.
        - Distribute the CNN across multiple devices.
- 456 — Pooling layers: the goal of these is to shrink the input image whilst retaining the most important features but reducing the computational load.
- 460 — Depth wise pooling in Keras/TensorFlow
    - Global average pooling — reduce the entire input down to a single value, very destructive, but can be very useful.
    - Typical CNN architecture: Input → Conv → Pooling → Conv → Pooling → Fully connected output
- 463 — LeNet-5 architecture
- 465 — Data Augmentation — image augmentation should be representative of a real transformation which can be learnable. For example, a human should be able to look at an image which has been augmented and not know that is has been augmented (thus the transformation being realistic).
- 471 — ResNet architecture
- 476 — SENet architecture (better performance than ResNet on ImageNet)
- 🔑 478 — Building a ResNet 34 architeture from scratch
- 🔑 479 — Using pretrained models from Keras
- 🔑 481 — Using pretrained models for Transfer Learning in Keras
- 🔑 482 — `tf.image` can be used with `tf.data` and is more efficient than `keras.preprocessing.image.ImageDataGenerator`, it can also use data from any source, not just a local directory
- 483 — Freezing layers at the beginning of training, then unfreezing layers after training for a little bit and lowering the learning rate
- 484 — Different image labelling tools
- 487 — Fully Convolutional Networks (FCNs)
- 489 — YOLO object detection
- 491 — Mean Average Precision (mAP)
- 492 — Semantic Segmentation
- 494 — Different Convolutional layers in TensorFlow such as `keras.layers.Conv1D` for sequences such as text or words

**Chapter 15: Processing Sequences Using RNNs and CNNs**

- 498 — Recurrent Neurons and Layers
- 501 — An RNN can take a sequence of inputs and output a sequence of outputs, this kind of network is referred to as a sequence-to-sequence network
    - There are also sequence-to-vector networks, vector-to-sequence networks and finally sequence-to-vector (encoder) followed by a vector-to-sequence (decoder) (called an Encoder-Decoder network)
- 503 — Forecasting a time series with tf.keras()
- 504 — Generating a time series using `generate_time_series()`
- 505 — Creating baseline metrics
- 507 — Stacking RNN layers into a Deep RNN, make sure to set `return_sequences=True` for each layer except the last one, so they’re connected to each other
- 510 — For a seq-2-seq network, use a TimeDistributed() layer to wrap the final Dense output layer
    - Note: The Dense layer can actually handle this on its own (no need for TimeDistributed()) but it’s more communicative to have it there
    - Note2: TimeDistributed(Dense(n)) is equivalent to Conv1D(n, filter_size=1)
- 513 — Creating an RNN cell with Layer Normalization from scratch
- 514 — Applying dropout in an RNN cell
- 516 — The LSTM cell
- 519 — The GRU cell
- 520 — Using 1D Convolutional layers to process sequences
- 522 — Coding up a simplified Wavenet architecture (full version in the notebooks)

**Chapter 16: Natural Language Processing with RNNs and Attention**

- 527 — Using Keras to get a file off the internet
    - How to split a sequential dataset
- 531 — Building and using a Char-RNN model
- 535 — Sentiment analysis with Keras
    - Sentence piece tokenisation
- 537 — Use `tft.compute_and_apply_vocabulary()` to automatically compute and apply a vocabulary across a corpus of text (from the TF Transform library)
- 539 — Creating word masks to tell a model to ignore certain words rather it having to learn which words should be ignored or not
- 540 — Reusing pretrained word Embeddings
    - 🔑 TensorFlow Hub makes it easy to use pretrained model components in your own models. These model components are called modules — [https://tfhub.dev](https://tfhub.dev)
    - TF Hub cache’s the downloaded files into the local system’s temporary directory.
        - You can fix this by setting the `TFHUB_CACHE_DIR` to the directory of your choice, e.g. `os.environ[“TFHUB_CACHE_DIR” = “./my_tfhub_cache”`
- 545 — TensorFlow Addons contains plenty of resources to help you build production-ready models such as encoder-decoder models
- 546 — Creating a bidirectional RNN layer in Keras
- 548 — Adding Beam Search with TensorFlow Addons
- 549 — Attention Mechanisms
- 552 — Visual attention and explainability
    - 📖 Explainability Paper — [https://homl.info/explainclass](https://homl.info/explainclass)
- 555 — The Transformer Architecture (a model built purely out of attention modules)
- 558 — Positional Embeddings layer in TensorFlow
- 559 — Multi-head Attention
    - 562 — Multi-head attention layer architecture
- 📖 563 — Find a Transformer tutorial here: [https://homl.info/transformertuto](https://homl.info/transformertuto)
- 📖 565 — Paper on Pervasive Attention: 2D Convolutional Neural Networks for Sequence-to-Sequence Prediction

**Chapter 17: Representation Learning and Generative Learning Using Autoencoders and GANs**

- 568 — Difference between autoencoders and GANs
- 571 — Simple autoencoder going from 3D to 2D
- 573 — Example of building a stacked autoencoder (multiple layers) for MNIST
- 576 — Using a stacked autoencoder to learn in an unsupervised way and then reusing the lower layers for a supervised network
- 579 — Convolutional autoencoders
- 586 — Variational Autoencoders
- 588 — Building a VAE for fashion MNIST
- 592 — Generative Adversarial Networks
- 599 — Building a DCGAN for fashion MNIST

**Chapter 18: Reinforcement Learning (skipped)**

**Chapter 19: Training and Deploying TensorFlow Models at Scale**

- 668 — Serving a TensorFlow Model using TensorFlow Serving (a fast and efficient way to serve models)
- 670 — Use `export ML_PATH=“$HOME/ml”` to setup a path to a certain directory, you can then access it using:
    - `cd $ML_PATH`
- 672 — Installing TF Serving with Docker
- 673 — Serving a model and querying it through a REST API
- 674 — Serving and querying a model through a gRPC API
- 675 — Deploying a new model version
- 677 — Creating a Prediction Service on GCP AI Platform
- 682 — Using and querying the prediction service you created with GCP’s AI Platform
- 683 — Creating a service account on GCP to make predictions with your model (restricted access)
    - Idea: Build app with Streamlit → Store model in GCS → Deploy Streamlit app with app engine (small one) → Query model through GCP AI Platform (or a Cloud Function?)
- 685 — Deploying your model to a mobile or embedded device (using TFLite)
    - 📖 If you’re looking for a book on machine learning for mobile and embedded devices, check out: TinyML: Machine Learning with TensorFlow on Arduino and Ultra-Low Power Micro-Controllers — [https://homl.info/tinyml](https://homl.info/tinyml)
    - 📖 Another book for practical applications of deep learning, such as on mobile and in the browser, check out Practical Deep Learning for Cloud, Mobile, and Edge — [https://homl.info/tfjsbook](https://homl.info/tfjsbook)
- 689 — Using GPUs to Speed Up Computations: using a single powerful GPU is often preferable to using multiple slower GPUs.
- 690 — 📖 If you’re looking to get your own GPU, a great blog post by Tim Dettmers may help with deciding — [https://homl.info/66](https://homl.info/66)
- 692 — Checking to see if a GPU is available using:
    - `nvidia-smi`
    - `tf.test.is_gpu_available()`
    - `tf.config.experimental.list_physical_devices(device_type=‘GPU’)`
- 694 — Managing the GPU RAM: TensorFlow automatically grabs all of the available RAM in a GPU to train a model, if you need to run two training sessions in parallel, you’ll need to split the RAM on the device (or assign the multiple GPUs on your machine each to a different process)
- 699 — Parallel execution across multiple devices: taking advantage of TensorFlow’s parallelism
- 701 — Tips for training with GPUs
- 701 — Training a single model across multiple devices
    - Model parallelism — model gets divided across multiple machines
    - Data parallelism — data gets divided across multiple machines (generally easier and more efficient)
- 710 — Using `tf.distribute.MirroredStrategy()` to distribute a Keras model training across multiple GPUs
- 715 — How to run a large-scale training job on Google’s Cloud AI Platform
- 716 — Using Google’s Bayesian optimisation hyperparameter service on AI Platform to improve your models performance

**Appendix A: Exercises**

- 733 — Leaky ReLU & SELU generally outperform ReLU, but ReLU is the simplest to use
- 739 — CNNs are more efficient than DNNs since they often don’t have as many connections
- 740 — Calculating the amount of RAM your CNN needs
- 742 — Applications of RNNs:
    - Sequence-to-sequence: predicting the weather, machine translation
    - Sequence-to-vector: classifying music samples by music genre, analysing the sentiment of a book review, recommender systems
    - Vector-to-sequence: image captioning, creating a music playlist based on an embedding of the current artist, locating pedestrians in a video
- 743 — LSTM cell breakdown
- 744 — Example of how you could classify video content
- 751 — TF Serving allows your models to become available through a REST API or gRPC API

**Appendix B: Machine Learning Project Checklist**

- 🔑 755 — The Machine Learning Project Checklist
    1. Frame the problem and look at the big picture.
    2. Get the data.
        - Automate as much as possible so you can easily get fresh data.
    3. Explore the data to gain insights.
    4. Prepare the data to better expose the underlying data patterns to Machine Learning algorithms.
        - Work on copies of the data (keep the original intact).
        - Write functions for all data transformations you apply, for reproducibility.
        - Fix or remove outliers (optional).
        - Fill in missing values or drop their rows.
        - Drop the attributes that provide no useful information for the task.
        - Discretize continuous features: put them in buckets.
        - Decompose features (e.g. categorical, date/time, etc).
        - Add promising transformations of features (e.g. log(x), sqrt(x), x^2, etc).
        - Aggregate features into promising new features.
        - Feature scaling: standardise or normalise features.
    5. Explore many different models and shortlist the best ones.
        - Try many quick-and-dirty models from different categories using standard parameters.
        - For each model, use N-fold cross-validation and compute the mean and standard deviation of the performance measure on the N folds.
        - Analyse the types of errors the models make.
            - What data would a human have used to avoid these errors?
        - Perform a quick round of feature selection and engineering.
        - Perform one or two more quick iterations of the five previous steps.
        - Short-list the top three to five most promising models, preferring models that make different types of errors.
    6. Fine-tune your models and combine them into a great solution.
        - For this step, use as much data as possible.
        - Always automate what you can.
        - Treat your data transformation choices (e.g. replacing missing values with mean, median or drop the rows) as hyperparameters.
        - Prefer random search over grid search and if training is very long, you might want to look into using a Bayesian optimisation approach.
        - Try ensemble methods, combining your best models will often produce better performance than running them individually.
        - Once you’re confident about your final model, measure its performance on the test set to estimate the generalisation error.
    7. Present your solution.
        - What worked, what didn’t?
        - How does your solution stack up against business metrics?
    8. Launch, monitor and maintain your system.
        - Remember, models start to “rot” as data evolves, retrain your models on a regular basis on fresh data (automate as much as possible).

**Appendix F: Special Data Structures In TensorFlow**

- 783 — Strings in Tensors
- 784 — Ragged Tensors: a special kind of tensor that represents a list of arrays of different sizes, a tensor with one or more ragged dimensions.
- 785 — Sparse Tensors: tensors containing mostly zeros, used for processing data efficiently.

**Appendix G: TensorFlow Graphs**

- 791 — TF Functions and Concrete Functions
- 794 — Example of a computation graph
- 798 — Wrap global variables in classes instead of defining them as they are
- 798 — Avoid using Python’s `'=', '+=', '-='` with TensorFlow Variables, using `assign(), assign_add(), assign_sub()` instead

**Index**

- 801 onwards — Index Terms
