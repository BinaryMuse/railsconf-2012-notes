Practical Machine Learning and Rails
====================================

What is Machine Learning
------------------------

* Predict data from other data
* What do you do with data?
  * Classify - categorize
    * Documents
      * Sorting
      * Routing
      * Categorization
    * Users
      * Expertise, excepted behavior, etc
    * Links
    * Etc.
* Algos
  * Decision tree learning
    * Straightforward
    * Number of words, presence of data, etc.
    * Decide what features best divide your data
  * Support vector machines
    * Useful for fewer than say 2000 features, e.g. if words are features, documents may not work well
    * Find a line/curve that best divides features
    * Data space may have many many vectors
    * libsvm
  * Naive Bayes
    * Good for text
    * Works well with a lot of data and a lot of features
    * Basis of most spam filters
    * Simple, can implemenet manually easily
    * Break document into words, treat each as completely independent feature
  * Neural nets
    * Speaker warned audience away from neural nets, in favor of support vector machines
    * Provably complete
    * Modeled after human brain at high level, hard to understand
    * Have a lot of caveats
    * Tendency to over-fit data, black magic as to how you pick data/nodes
* Curses of dimensionality
  * The more features and levels you have the more data you needt to successfully classify
* Overfitting
  * With enough parameters, anything is possible
  * Don't want algo to memorize, but generalize
  * Test on different data that you train on to avoid overfitting
* Algo tends to learn simplist thing it can, or gravitate to biases
  * (Cloud detector example)

2nd half: Practical Machine Learning
------------------------------------

* Sentiment Classification/Sentiment Analysis
  * Is block of text positive or negative
  * Training set (ex: tweets)
  * Use emoticons as lables, search directly from :) and :(, remove from tweet, and use that as label
  * Extract features for algo (ex: bag of words model, converts text into features, ignores grammar/sentence structure)
    * Split into words, create dictionary of words in all training examples, keep certain number of those, e.g. top 10,000
    * Replace text with counts:

          I ran fast
          Bob ran fast
          I ran to bob

      Change into word vectors
    * Take word vectors and levels and feed into algo
    * Algo spits out model that you can query with new examples
  * Open source tool: weka
    * Java app
    * Contains common machine learning algos
    * Helps with words -> word vectors, training test set, etc.
    * Gives metcrics
  * ARFF file - similar to CSV, with more header info
  * (demo)
  * Evaluation
    * Basic:Number correctly classified
    * Regression: look at mean absolute error and mean square error
    * Unbalanced data set (common in machine learning), look at confusion matrix
      * Tell you how many it guessed in each class
      * Gives you idea of false positives and negatives
  * http://github.com/ryanstout/mlexample - JRuby example
  * How do we improve?
    * Have bigger dictionary
    * Use bi-grams and tri-grams (text specific)
      * Bi-grams pick up negations ("don't like")
    * Part-of-speech tagging, treat same words that are different parts as different features
    * Have more data
* Feature Generation
  * Ask expert about what features they'd use
  * Remove data that isn't useful - "attribute selection"


Example: Domain Price Prediction
--------------------------------

  * Training data set
    * Domain name
    * _Historical_ price of domain on resell markets
  * Features: split into words, generate features for each word
    * How common it is
    * Google search results
    * Cost per click to advertise on word
  * Feed into regression algo, "support vector regression"

What Wasn't Covered
-------------------

* Collaborative filtering
  * E.g. recommendation engines
* Clustering
  * System gruops features based on some similarities
  * Grouping documents (e.g. Google News), related terms
* Theorem Proving

For more info check out free Stanford machine learning class at ml-class.org

Tools
-----

* Ruby bindings for libsvm and liblinear
* If you use these, you don't get metrics, etc. like weka
* Vowpal wabbit - handles large data set easily
* Recommendify - collaborative filtering
