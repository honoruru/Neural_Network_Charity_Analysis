# Neural_Network_Charity_Analysis

## Overview 

The purpose of the project is to create a binary classifier that is capable of predicting whether applicants will be successful if funded by Alphabet Soup.


## Results

The initial step in creating the classifier is to preprocess the data in charity_data.csv.  

### Data Preprocessing
The IS_SUCCESSFUL variable is considered the target for our model.

The EIN and NAME variables are considered neither targets nor features and were removed from the input data.

This left the following remaining variables which are considered to be the features for the model:

APPLICATION_TYPE          object
AFFILIATION               object
CLASSIFICATION            object
USE_CASE                  object
ORGANIZATION              object
STATUS                     int64
INCOME_AMT                object
SPECIAL_CONSIDERATIONS    object
ASK_AMT                    int64

For the CLASSIFICATION feature, value counts less than 1,000 were binned.  For APPLICATION_TYPE, value counts less than 500 were binned. 

The features that were objects were transformed into encoded columns using OneHotEncoder.

### Compiling, Training, and Evaluating the Model

The initial classifier model comprised two hidden layers as shown below:

|Layer        | # Neurons   |Activation |
|-------------|-------------|-----------|
| Hidden 1    | 80          |ReLU       |
| Hidden 2    | 30          |ReLU       |
| Output      | N/A         |Sigmoid    |

The number of hidden layers and neurons were provided as initial guidance by the clients.  The ReLU activation function was selected for the hidden layers as it is ideal for looking at positive nonlinear input data for classification or regression.  The Sigmoid activation function was selected for the output layer as it is ideal for binary classification. 

The initial model did not achieve the target predictive accuracy higher than 75%.  A number of changes were attempted to improve the model to increase its accuracy.  These included increasing the neurons, epochs, and activation functions.  One attempt was made with lower bin thresholds.  None of the attempts resulted in a model that achieved target predictive accuracy.

|hn1|hn2|act1|act2|act3|model_loss|model_accuracy|epochs|app_typ_bin|CLASS_bin|
|---|---|---|---|---|---|---|---|---|---|
|80|30|relu|relu|sigmoid|0.560406506|0.72559768|50|500|1000
|80|30|relu|relu|sigmoid|0.560330272|0.727463543|100|500|1000
|100|50|relu|relu|sigmoid|0.567526042|0.724081635|100|500|1000
|80|30|relu|relu|sigmoid|0.558836699|0.7252478	100|50|100
|8|3|relu|relu|sigmoid|0.554078162|0.723498523	100|500|1000
|80|30|relu|relu|sigmoid|0.56947726|0.724664748|200|500|1000
|80|30|relu|relu|sigmoid|0.563939214|0.725714266|100|500|1000
|80|30|tanh|relu|sigmoid|0.561141253|0.725131214|100|500|1000
|100|50|tanh|relu|sigmoid|0.57213223|0.724781334|100|500|1000


Several attempts were made with a third hidden layer without success. 

|hn1|hn2|hn3|act1|act2|act3|act4|model_loss|model_accuracy|epochs|
|---|---|---|---|---|---|---|---|---|---|
|100|50|50|relu|relu|relu|sigmoid|0.568680584|0.725481033|50
|100|50|50|relu|relu|relu|sigmoid|0.576114714|0.726413965|100
|100|100|100|relu|relu|relu|sigmoid|0.601408184|0.725364447|100
|80|30|30|relu|relu|relu|sigmoid|0.567723036|0.724664748|100
|100|50|50|relu|relu|relu|sigmoid|0.600123882|0.724548101|200
|100|50|50|tanh|relu|relu|sigmoid|0.577502072|0.7252478|100
|100|50|50|tanh|relu|relu|relu|0.612268388|0.72326529|100

As with the two-layer models, none achieved predictive accuracy of even 73%.

## Summary

The following observations were made based on changes to the initial model.
1.	Increasing epochs from 50 to 100 provided as slight improvement in accuracy, however, increasing the epochs to 200 did not.
2.	Changing the activation function of the first hidden layer to Tanh did not result in a notable improvement.
3.	Decreasing the bin thresholds to included more value counts did not result in a notable improvement.
4.	Adding an additional hidden layer did not result in a notable improvement.
5.	One attempt was made with the two-layer model with significantly less neurons.  This produced the worse result other than a three-layer model that used ReLu as the activation function for the output layer.

For future attempts at improving the model’s performance, it is recommended that one stay with a two-layer model as three layers appeared to provide no benefit.  The activation function of the output layer should remain Sigmoid, however other functions should be attempted for the two hidden layers.  Finally, after a closer analysis of the features, it may be beneficial to remove certain ones as they may not be helpful in prediction and may, in fact, be adding a conflicting component to the model. 

