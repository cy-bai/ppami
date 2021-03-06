# Code and dataset for M2P2: Multimodal Persuasion Prediction using Adaptive Fusion

----
## Code
### Dependencies
python 3: PyTorch (tested on 1.5.0), numpy, scipy, pandas. 

### Run
Download *qps\_dataset.tar.gz*, extract it, and put the extracted *qps\_dataset* folder under the root folder.

Create a folder to save your own trained models:
```bash
mkdir new_trained_models
```

To test the performance of our pre-trained model, run
```bash
python main.py --test_mode --fd=FOLD
```
The MSE loss in the test set of fold FOLD will be printed.

To train the model we proposed, run
```bash
python main.py --het_module --fd=FOLD --verbose
```
This will train the model for fold FOLD and output the concat weights as well as training and validation loss every 2 epochs (if enabling *verbose*), the trained model and concat weights  will be saved in *new\_trained\_models/fold[FOLD]/*.

### Code details
* main.py. Executes the training / testing of the whole work.

* dataset.py. Loads raw features from all modalities to pytorch.

* model.py. Our model for learning latent embeddings, making predictions and reference models.

* train.py. Training and Evaluation functions for all prediction models and reference models.

* utils.py. Utility function, defined constants and hyperparameters.

* folds_split/. Stores the segments used for training, validation and test in each fold.

* models/. Save pre-trained models and concat weights for each fold.

## QPS dataset
*qps\_index.csv* stores the meta-data of the whole dataset, including the columns: debate episode ID ("deb"), clip ID ("clip"), segment ID ("seg_id"), change of votes ("change"), post vote ("ed_vote"), clip length ("dur_sec"), etc.

Download and extract *qp_dataset.tar.gz* to get the dataset. Inside, each folder represents a segment corresponding to *qps\_index.csv* by the "seg_id" column. 

In each segment folder, *covarep\_norm.npy* is the extracted COVAREP audio features, *tencent\_emb.npy* is the extracted word embeddings, and *vgg_1fc* stores the extracted features of each frame extracted from the pre-trained CNN without the last FC layer. We use these features as input to get the primary input embeddings.

**Now we have only released the raw features. We are working on getting the license and copyright from iQIYI. We will release the original videos once getting their approval.**
