# Protein Function Prediction
2023-2424 Bio Data Group 8 Final project

*Angela Kralevska (2072021), Elena Stefanovska (2085310), Cameron Kelahan (2071947)*

This is a repo for the final project for the Biological Data course. For ease, the repo can be eithe rcloned and run locally or implemented in google colab.

The prediction software is made up of 6 different python notebooks:
 * data_processing.ipynb
 * MLP_T5_domains_data_Biological_Process.ipynb
 * MLP_T5_domains_data_Molecular_Function.ipynb
 * MLP_T5_domains_data_Cellular_Component.ipynb
 * Kfold_CV _MLP_T5_domains_data.ipynb
 * Make_predictions.ipynb

The data to be used by the software is found at [this link](https://drive.google.com/drive/folders/196iOpk3-GAwI6yb57b3DYyDhxCn8t1Zo?usp=sharing). Download and unzip the folder, then move it into this directory (BioDataFinalGroup8). This file will need to be accessed from this local location.

## Executing the code

### Open the **data_processing.ipynb** notebook

This notebook handles the processing of the data into ready-to-use files. You **must specify the PATH variable** to be the location of the 'biilogical_data_pfp' folder that you previously unzipped and placed in this directory. After doing so, run the file to completion. At the end, you will have generated the following files:

 * train.tsv: training set used by all models to train on
 * validation.tsv: used by all models as a validation set while training
 * train_embeddings.npy: numpy array version of the train_embeddings.h5 file values
 * test_embeddings.npy: numpy array version of the test_embeddings.h5 file values
 * train_ids.npy: numpy array version of the train_embeddings.h5 file protein IDs
 * test_ids.npy: numpy array version of the test_embeddings.h5 file protein IDs
 * domain_embeddings_pca.npy: numpy array containing the PCA of the InterPro domain values for the training set
 * test_domain_embeddings_pca.npy: numpy array containing the PCA of the InterPro domain values for the test set
 * domain_embeddings_pca_ids.npy: numpy array containing the protein IDs of the training set domain_embeddings_pca.npy values
 * test_domain_embeddings_pca_ids.npy: numpy array containing the protein IDs of the test set test_domain_embeddings_pca.npy values
 * train_set_ia.tsv: file containing the calculated information accreation (IA) values of the training set

### Open one of the MLP_T5_domains_data_* Notebooks

All three of these notebooks (Biological_Process (BP), Molecular_Function (MF), and Cellular_Component (CC) are organized in the same way. Execution order does not matter.
Again, you **must specify the PATH variable** to be the location of the 'biilogical_data_pfp' folder that you previously unzipped and placed in this directory for **each** of these 3 notebooks. After doing so, run the files to completion.

Each file contains the same sections:
 * Load and combine the data to make the training and validation datasets for the specific aspect (BP, MF, or CC)
 * Plot the Most frequent GO terms for the specified aspect
 * Create a matrix of go proteins and their go terms through one-hot encoding to act as the ground truth labels for the training (each protein is a row, each column a go term; if the protein is associated with a go term, that (row,column) will have a 1; if there is no association it will have a 0)
 * Train the model; it runs for 50 epochs
 * Save the model for future use and evaluation
 * Perform some analysis of the model by calculating the Precision, Recall, and F1 Score of the training and validation sets
 * Plot confusion matrices for the first and last 15 terms in both the training and validation sets
 * Plot the ROC curves for the first and last 15 terms in both the training and validation sets

**The Cellular_Component notebook has an additional functionality at the end.** Althought our computing resources were limited, the CC dataset was successfully run on the CAFA-evaluator. The bottom section of code executes this and gives an F1 score based on the evaluation.

### 

Output from the **contacts_classifier.py** script:
- Example on how the output from our software looks like can be observed at the **2ghv.tsv file**.
- The last three columns represent the predictions from the model.
- The column named **model_predictions** contains the predictions made from the model in a list of 1s and 0s (where 1 means that the class is predicted, and 0 means that the class is not predicted), such that the classes are ordered in this way -> ["HBOND", "IONIC", "PICATION", "PIPISTACK", "SSBOND", "VDW"].
- The column named **prediction_scores** represents the probabilities outputed from the model, i.e. the confidence scores for its predictions, and they are ordered in the same order as in the **model_predictions** column -> ["HBOND", "IONIC", "PICATION", "PIPISTACK", "SSBOND", "VDW"].
- The last column **predicted_classes** contains list of the names of the predicted classes only.

Instructions for reproducing the model:
- The model can be reproduced by executing the **Final_Model_Training.ipynb** notebook on Google Colab. Make sure to change the **path** variable before executing.
- The dataset used for training can be obtained from this link (https://drive.google.com/file/d/1vuIvAs_rdM-hfeePw7gPhe2TWJKbXf9k/view?usp=sharing), it couldn't be attached on github because it is larger than 100MB. The dataset should be placed in the folder specified at the **path** variable.
- The model will be saved as **final_model.h5** at the same folder specified at **path**.

Our report can be found in the **SB_Project_Report.pdf file**.

All experiments and evaluation with the DNN model for multi-label classification are available in the **DNN_experiments.ipynb** notebook. In addition, this notebook contains the final code and plots regarding the EDA (Exploratory Data Analysis) steps as well as the code for calculating the new features and generating the final clean dataset with all features together. Moreover, the code and experiments with MLSMOTE oversampling are included.

Experiments with OneVSRest approach for classification and obtaining feature importance by training Random Forest model are available in the **OneVSRest_and_Feature_importance_experiments.ipynb** notebook. 
