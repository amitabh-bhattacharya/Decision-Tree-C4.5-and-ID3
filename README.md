## Decision tree (C4.5 and ID3):

In this project, I implemented two decision tree classifiers, Quinlan’s ID3 and C4.5 as defined in our lecture. Once implemented, they are experimented on the Mushroom dataset from the University of California Irvine Machine Learning Repository.

I used the UCI Mushroom (https://archive.ics.uci.edu/ml/datasets/mushroom) datasets for this project. This dataset contains about 8124 mushroom examples over 22 categorical attributes, with each example labeled either edible ("e") or poisonous ("p"). In this dataset, there are 4208 (51.8%) edible examples and 3916 (48.2%) poisonous examples. For our experiments once the decision tree model is implemented, this dataset is randomly split to a training set of 80% and a testing set of 20%. Both have very similar distribution: 51.9% edible and 48.1% poisonous for the training set, and 51.4% edible and 48.6% poisonous for the testing set. 

### Requirements fulfiled

1. The program implements Quinlan’s ID3 and C4.5 decision tree learning algorithms, where the IMPORTANCE method would be based on information gain and gain ratio, respectively.

2. For both ID3 and C4.5, the program implements a 10-fold cross validation process over the training set, the best model is picked with the highest F1 score.

3. Finally it is run on the testing set and the F1 score is reported.

4. To ensure non-randomness, the 10 partitions used in cross validation are provided as 10 files in Data folder.

## Program explanation:

###	Classes:

Node - 
The decision tree. The tree is built using Node class object. The class object can be either an internal node of the tree or a leaf. If the Node object is an internal node then instance variable "name" would contain the name of the attribute/feature in the corresponding train dataset on which the tree is split. The "branch_names" contains the attribute values. The instance variable "branches" contains the references to sub-tree. If the node is a leaf then the "decision" contains the final decision upon landing to the leaf while traversing the decision tree. Make a note that a node cannot be simultaneously an internal node as well as a leaf so either "name" or "decision" would contain a null value for a node.

The Node class has a class function predict(df) and row_predict() which is used to make a prediction. predict(df) function takes a dataframe as input and iteratively calls row_predict() function for each row of the dataset.

The print() function prints the tree on which it is called. 

###	Methods: 

1.) fit_dt(df, algorithm) - 
This is the function that creates the decision tree and gets trained on the training dataset provided as input (df here). algorithm can take 2 possible values i.e. 'id3'/'c4.5' and the default is 'id3'. It implements the Quinlan's ID3/C4.5 decision tree respectively. The output of the function is the reference to the root node of the trained tree.

2.) entropy(series) -
This function takes a series as input and computes/returns the entropy of the collection as output. This function is frequently called from other functions like info_gain() or gain_ratio() to obtain the entropy information.

3.) info_gain(current_entropy, attribute, df) -
This function computes the information gain if the tree is split on the attribute of df dataset. The information gain is entropy of teh child subtracted by entropy of the current position. Current position's entropy is provided as input current_entropy. Entropy of a collection is computed by using the entropy() function explained above.

4.) gain_ratio(current_entropy, attribute, df) -
The gain ratio is a little extension to the info_gain(). Gain ratio is given as information gain divided by intrinsic value.Gain ratio is used by C4.5 algorithm and the basic idea is to favor attributes that has lesser values.

5.) validation(train_list) -
The validation function is used to find the tree that provides best score on a validation dataset getting trained on a particular training dataset. The input to the function is a list of dataset. One is picked, in round robin fashion, to be the validation set and the remaining are merged to form a training set for the training of the tree.

The output of the validation function is the tuple with references of the trees (id3 & c4.5) having best f1 score over a validation set.

###	Running steps:

1.) Run the Decision_tree.ipynb in Jupiter notebook.
2.) The training/test dataset is available in Data folder. Note that training data is divided in 10 equal parts for cross validation. At each iteration of cross validation we use 9 training dataset and reserve the last for validation.
3.) The program imports all the training/testing dataset as step 1
4.) At step 2 it prepares two best trained trees (id3 & c4.5).
5.) At step 3 it computes and outputs the F1 score for both trees using test dataset.

###	Final output:
F1 score on test dataset using id3 algorithm is:  1.0
F1 score on test dataset using C4.5 algorithm is:  1.0

