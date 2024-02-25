# Protein Function Prediction
2023-2424 Bio Data Group 8 Final project

*Angela Kralevska (2072021), Elena Stefanovska (2085310), Cameron Kelahan (2071947)*

This is a repo for the final project for the Biological Data course. For ease, the repo can be either cloned/downloaded and run locally or implemented in google colab.

The prediction software is made up of 6 different python notebooks:
 * data_processing.ipynb
 * MLP_T5_domains_data_Biological_Process.ipynb
 * MLP_T5_domains_data_Molecular_Function.ipynb
 * MLP_T5_domains_data_Cellular_Component.ipynb
 * Kfold_CV _MLP_T5_domains_data.ipynb
 * Make_predictions.ipynb

The data to be used by the software is found at [this link](https://drive.google.com/drive/folders/196iOpk3-GAwI6yb57b3DYyDhxCn8t1Zo?usp=sharing). Download (and unzip the folder if necessary), then move it into this directory (BioDataFinalGroup8). This file will need to be accessed from this local location.

Our final version of the trained models are contained in the biological_data_pfp/models directory. Please access them here for testing.

**The final submission.tsv file we are submitting for testing is found in the root of this repository.**

## Executing the code to train from scratch

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

### Optional Kfold_CV _MLP_T5_domains_data.ipynb Notebook

This notebook creates the models while utilizing KFold Cross Validation.

### Making predictions and creating the submission.tsv file

Open the final notebook, Make_predictions.ipynb. This notebook simply loads the three previosuly created models and records their predictions on the test set given in the biological_data_pfp/test directory. The submission.tsv file is output containing a list of protein/GO-term pairs and the proability that the specified GO-term is associated with the matched protein. No protein can have more than 1500 GO-terms associated with it across the 3 sub-ontologies. This file can be used for testing the performance of our software.
