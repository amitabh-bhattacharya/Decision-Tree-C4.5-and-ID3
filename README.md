## Decision tree (C4.5 and ID3):

In this project, Quinlan’s ID3 and C4.5 decision tree classifiers are implemented using python language. Once implemented, they are experimented on the Mushroom dataset (https://archive.ics.uci.edu/ml/datasets/mushroom) from the University of California Irvine Machine Learning Repository. The methods used for ID3 and C4.5 are Information Gain and Gain ratio respectively. For both ID3 and C4.5, the program implements a 10-fold cross validation process over the training set and the best model is picked with the highest F1 score.

#### I have taken advantage of pandas dataframe to prepare (train) the tree. This is a novel and a very convinient way to operate on a dataset with millions of features and/or records. Obtaining a subset (column or row wise) of a dataframe is very easy that is a primary aspect to train a decision tree.

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
