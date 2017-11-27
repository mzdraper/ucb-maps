# Maps

## Overview
This Python project is a visualisation of restaurant ratings using machine learning and the [Yelp academic dataset](https://www.yelp.com/academic_dataset). This projects Berkeley into segmented regions, where each regin is shaded by the predicted rating of the spatially closest restaurant. It is further coded with yellow being 5 stars and blue being 1 stars. The visualisation that appears is a Voronoi diagram.

Dots on the map are repsesentitve of restaurants. They're coloured depending on their spatial relationship to others, or clustering. For example, the green dots are those clustered in Downtown Berkeley and the blue dots are those notrh of UC Berkeley's campus.

This repo contains all the documents for completing this project. Each file's respective responsibility is as follows:
   * abstractions.py: Data abstractions used in the project
   * recommend.py: Machine learning algorithms and data processing
   * utils.py: Utility functions for data processing
   * ucb.py: Utility functions for CS 61A
   * data: A directory of Yelp users, restaurants, and reviews
   * ok: The autograder
   * proj2.ok: The ok configuration file
   * tests: A directory of tests used by ok
   * users: A directory of user files
   * visualize: A directory of tools for drawing the final visualization

## Phase 0: Utilities
### Problem 0
All changes are made in `utils.py`
#### Problem 0.1: Using List Comprehensions
A list comprehension comprehension constructs a new list from an existing sequence. It filters the given sequence, then computes an element of the result for each remaining element that is not filtered out. The syntax looks the following:
`[<map expression> for <name> in <sequence expressions> if <filter expressions>]`

What: `map_and_filter` function 
Functionality: Takes in a sequence `s`, a one-argument function `map_fn` and a one-argument function `filter_fn`
Returns: a new list containing the result of calling `map_fn` on each element of `s` for which `filter_fn` returns a true value

#### Problem 0.2: Using `min`
The `key` function is a one-argument function that is called with each element of the list, and the return valies are used for comparison.

What: `key_of_min_value` function

Functionality: takes in a doctionary `d`
Returns: key that corresponds to the minimum value in `d`

#### Problem 0.3 Using `zip`
The `zip` function take multiple sequences as arguments and returns lists of lists, where the n-th list contains the n-th element from the original list. 

* What: `enumerate` function
* Functionality: takes a sequence `s` and a beginning index `start`
* Returns: a list ofpairs, where the n-th element is `n+start` paired with the n-th element of `s`

### Problem 1
* What: `mean` function
* Functionality: takes in a sequence of numbers
* Returns: arithmetic mean

## Phase 1: Data Abstraction
All changes are made in `abstractions.py`
### Problem 2
* What: `make_restaurant`, `restaurant_name`, `restaurant_location`, `restaurant_categories`, `restaurant_price`, `restaurant_price`, `restaurant_ratings`
* Functionality: Completes the implementations of the constructure and selectors for the restaurant data abstraction

## Phase 2: Unsupervised Learning
All changes are made in `recommend.py`

The **k-means algorithm** discovers the centers of clusters. It finds `k` centroids within a dataset that each correspond to a cluster of inputs by randomly selecting a `k` centroid and testing it.

### Problem 3
* What: `find closest` function
* Functionality: takes a `location` and a sequence of `centroids`
* Returns: element of `centroids` closet to `location`

### Problem 4
* What: `group_by_centroid` function
* Functionality: takes a sequence of `restaurants` and a sequence of `centroids`
* Returns: list of clusters (order does not matter)

### Problem 5
* What: `find_centroid` function
* Functionality: finds the centroid of a cluster based on the locations of the restaurants using the centroid's latitude and longitude
* Returns: the centroid of the cluser

### Problem 6
* What: `k-means` function
* Functionality: grouping `restaurants` into clusters of the same centroid and binding `centroids` to a new list
* Returns: `centroids`

## Phase 3: Supervised Learning
All changes are made in `recommended.py`
### Problem 7
The *simple least squares linear regression* is a statistical method that approximates the relationship between some input feature and an output value within a line. In a relevant example, it would approximate the correlation to price and rating. It finds the approximation by computing the slope and interept of the line that minimizes the mean of the squared difference between the line and the outputs.

* What: `find_predictor` function
* Functionality: takes in a `user`, a sequence of `restaurants` and a feature function `feature_fn` and finds their relationship using the simple least squares linear regression
* Returns: a `predictor` function and an `r_squared` value

How to compute the simple least squares linear regression is within the code itself.

### Problem 8
* What: `best_predictor`
* Functionality: uses each feature function to compute a predictor function
* Returns: the predictor that has the highest `r_squared` value

### Problem 9
* What: `rate_all` function
* Functionality: takes a `user` and a list of `restaurants` and creates an empty dictionary and fills it out based on review status
* Returns: returns a dictionary where the keys are the names of each restaurant in `restaurants`

### Problem 10
* What: `search` function
* Functionality: takes a category `query` and a sequence of restaurants and filters them through a list comprehension
* Returns: all restaurants that have `query` as a category

`-q` allows you to filter based on a category.

Try running the following to see a visualisaition of all sandwich restaurants and their predicted ratings for the user who `likes_expensive`:
> python3 recommend.py -u likes_expensive -k 2 -p -q Sandwiches

## How to predict your own ratings
In the users dictionary, there are .dat files. Personally, I don't know how to open--let alone--these files. However, you can edit your own reviews of restaurants and get your predictions!

## Testing
In order to test your code through the `ok` grader, you have to first pass a series of tests. The tests are simple in that they're just confirming you truly understand what the functions are supposed to do before you write them. Expect a lot of tests!

To begin the tests, type `python3 ok -u` into the terminal. Once you would like to test your own code, type in `python3 ok`. Use `python3 ok -q function-name>` for testing specific parts of your code. The tests may annoyingly ask for your Berkeley credentials, so you may want to type `--local` whenever envoking ok.

## The Actual Project
This doument has been my interpretation of the original scaffolding, so it may be bare in some areas and extensive, depending on my familirity. Thus, I haven't gone through each grueling detail, as I feel the code and supplementary comments should be sufficient. But if you would like the original scaffolding, [certainly](https://cs61a.org/proj/maps/) "happy mapping".
