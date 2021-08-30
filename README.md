# Neural_Network_Charity_Analysis  
  
### Overview of the analysis:  
  
The purpose of the analysis is to create a neural network that determines if an applicant for funding through Alphabet Soup will be successful.  The model is trained and tested on splits from a csv file of 34,299 historic projects.  
  
A successful model has 75% or higher accuracy when applied to the testing split of the data.  If model optimization does not reach 75% accuracy then 3 good faith attempts are considered adequate to satisfy the criterion. 
  
### Results:  
  
#### Data preprocessing:  

- The input data contains a binary column for project success.  The model target is the "IS_SUCCESSFUL" column.  
  
- Nine columns of the initial csv file are the features for the model:  
  - APPLICATION_TYPE:  17 categorical values (unknown meaning to the analyst)  
  - AFFILIATION:  6 possible affiliations (including other)  
  - CLASSIFICATION:  70 categories (unknown meaning to analyst)  
  - USE_CASE:  5 cases (including other)  
  - ORGANIZATION:  4 types of organizations  
  - STATUS:  1 or 0 for active or inactive  
  - INCOME_AMT:  Ranges of income of the organizations that were funded.  
  - SPECIAL_CONSIDERATIONS:  yes or no
  - ASK_AMT:  how much money was requested and granted.  
  
- There are 2 columns of the csv file that are not helpful for the analysis:  EIN and NAME.  

#### Compiling, Training, and Evaluating the Model:  
  
- The initial model contains 2 hidden layers with relu activation and an output layer with sigmoid activation.  The model runs for 50 epochs.  The first hidden layer has 27 neurons (3* number of input columns prior to encoding).  The second hidden layer has 14 neurons (approximately 1/2 of the first hidden layer).  These parameters are an attempt to be consistent with neural network rules of thumb.  
  
- The initial model accuracy was 0.7300.  This does not meet the criterion of 75% accuracy.  
  
- The first attempt to optimize the model was running a loop on a single hidden layer.  The model looped through the number of neurons in the hidden layer:  from 50 to 60.  The best accuracy was 0.7324 (54 neurons).  The agreement in accuracy between the initial 2 hidden layer model and this test suggests that the poor performance is not a result of non-linearity.  The second attempt was to run a set of nested loops for a 2 hidden layer model with relu activation and 50 epoch run.  THe outer loop controls the number of neurone (50 to 60) and the inner loop controls the number of neurons in the second hidden layer (25 - 30).  The best accuracy was 0.7324 for the model with 52 neurons in the first hidden layer and 27 in the second hidden layer.  The third attempt to optimize the layer is the same set of loops as the second attempt with the activation on the hidden layers changed to elu.  The highest accuracy was 0.7343.  
  
The best best model run is saved as "AlphabetSoupCharity_Optimization.h5".  The weights from every 5th epoch are saved in the chcekpoints folder.  
  
The initial model run is saved as "AlphabetSoupCharity.h5  
  
### Summary:  
  
A deep learning model (2 hidden layers) was trained with 50 features.  The features were encoded from 9 columns of data in the intial data file.  The attempts to optimize the model did not result in an accuracy of 0.75 or better.  

There was no appreciable change in the model accuracy going from a single hidden layer to 2 hidden layers.  This likely indicates that the poor model results are not the result of non-linear relationships in the data.  As such, using a tool like a logistic regression could get equal or superior performance with less computational cost.    


