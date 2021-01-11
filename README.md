# fiery future Remote Sensing of Environment experimentss

This repo is python 2 with an older version of Tensorflow. Details can be found in fiery.yml

## Setup
$ conda env create -f fiery.yml

## Files
+ classify_dnn.py
    - Script for running a single DNN experiment
+ classify_lr.py
    - Script for running a single Logistic Regression experiment
+ classify_rnn.py
    - Script for running a single RNN experiment
+ graph_training_utils.py
    - Helper functions for boilerplate tensorflow training code
+ tf_ops.py
    - Tensorflow neural network modules
+ util.py 
    - There is a Batcher object that gets imported for batch gradient descent
+ best_get.py
    - This script is for going through the output files on remote runs to track down the best performing model.
    - It is a stop gap as I forgot to record the run number in the main output files so it goes through all the predictions
    - for model runs and recalculates the metrics. 
+ exp/
    - {DNN, RNN, LR, RF} Since the DNN and RNN models take longer to train there is a little difference between them and LR, RF
        + idxs: Dedicated indexes for train/test splits
        + clean_jan_field_data.csv: The training data reproduced in each experiment folder for convenience
        + create_slurm.py: Script that makes slurm dispatch files for splitting the experimental runs across gpus on marianas
        + split_{dnn, rnn}.py: Experimental script that runs a subset of experiments
        + ex_{dnn, rnn, lr, rf}_classify.py: For running all experiments on a single gpu sequentially 
+ mapping: 
    - dnn_d4_models/: Best performing DNN models
    - map_slurm_runs/
        + create_slurm.py: Creates slurm dispatch scripts for making the final map. Need to manually create fold{0,1,2,3,4} folders and logs subfolders
    - More to come explaining the other scripts
+ results_and_analysits:
    - results.ipynb: Digests results from allruns/ to find best performing models and associated metrics
    - allruns/: Files recording performance of all model runs
    - dnn_training/: training results for best performing DNN models
    - pics/: plots
    - predictions: Predictions for all best performing models for all data subsets. Numpy arrays with shape=(number_data_points, 4):
        + index 1: data point unique id
        + index 2: data point ground truth cheatgrass coverage estimate
        + index 3: model prediction for probability < 2% cheatgrass coverage
        + index 4: model prediction for probability >= 2% cheatgrass coverage
    - plot_roc.py: Plot roc curves
    - plot_training.py: Plot DNN training curves
 
