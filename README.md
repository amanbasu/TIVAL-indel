# TIVAN-Indel
A computational framework for annotating and predicting noncoding regulatory Small Insertion and Deletion (sindel).

By leveraging labeled sindel that are highly potential in regulating gene expressions in GTEx, as well as a compilation of both generic functional annotations and tissue-specific functional annotations generated by sequence-based deep learning models, we developed TIVAN-Indel, which is an XGBoost-based supervised framework for scoring noncoding sindels based on their potential to regulate the nearby gene expressions. 

<p align="center"><img src="res/overview.png"/></p>
<p align="center">Figure 1. Overview of the TIVAN-Indel.</p>

## Requirements

TIVAN-Indel uses python `3.9.6` and xgboost `1.5.1`. The other requirements are:

```
h5py==3.1.0
matplotlib==3.4.3
numpy==1.19.3
numpy-utils==0.1.6
pandas==1.4.0
scikit-learn==0.24.2
tensorflow==2.6.0
```

## Usage

Download TIVAN-Indel

```bash
git clone https://github.com/amanbasu/TIVAN-indel.git
```

Install requirements

```bash
pip install -r requirements.txt
```

### DanQ model

The trained weights of DanQ model are provided in the `checkpoint/` directory, while the model code is present in `models/` directory. You can train your own model by using data from DeepSEA website (http://deepsea.princeton.edu/help/).

<!--
You can learn more about the script arguments using the `-h` command for individual files

```
$ python train_base.py -h
usage: train_base.py [-h] [--type {pe,pp}] [--epochs EPOCHS] [--lr LR]
                     [--dropout DROPOUT] [--test TEST]

Arguments for training.

optional arguments:
  -h, --help         show this help message and exit
  --type {pe,pp}     interaction type
  --epochs EPOCHS    maximum training epochs
  --lr LR            learning rate
  --dropout DROPOUT  dropout
  --test TEST        test flag to work on sample data
```




### Train shared model

Shared models will use all the tissues for training as discribed in the Figure 1. When you train a shared model for one tissue, all the tissues will be used for training except that tissue, so that the training data does not leak into the testing data. All the shared models will be stored in the  `models/shared/` folder.

```bash
python train_shared_models.py --type pp --dropout 0.5 --test True
```

### Train fine-tune model

For training DeepPHiC-TL models. The model statistics (i.e. auroc, auprc, accuracy, fpr, and tpr) would be stored inside the `results/stats/` folder.

```bash
python train_finetune.py --type pp --lr 0.0001 --test True --train_full True
```

### Train multi-task model

For training DeepPHiC-ML models.

```bash
python train_multitask.py --type pp --lr 0.001 --test True
```

### Plot ROC curve

Reads the model statistics from the `results/stats/` folder and plots the ROC curves.

```bash
python plot_roc.py --type pp --tissue LV
```

<p align="center"><img src="results/plots/roc_curve_LV_pp.jpg" width="500px"/></p>
<p align="center">Figure 2. ROC curve for LV tissue for promoter-promoter (pp) interaction.</p>
-->
