# **TlcMHCpan**

**TlcMHCpan**: A Novel Deep Learning Model for Enhanced Pan-Specific Prediction of Peptide-HLA Binding Affinity

-------------------

This repository contains the code and the data to train **TlcMHCpan** model.

 Contact: [1299890870@qq.com](mailto:1299890870@qq.com); [solfix123@163.com](mailto:solfix123@163.com)

## Project Structure

### Dataset：All training and evaluation dataset.

- Benchmark data：A collection of data ranging from June 21, 2019, to August 3, 2023(source: http://tools.iedb.org/auto_bench/mhci/weekly）

- proteins：Training dataset sourced from https://github.com/uci-cbcl/HLA-bind

- BD2013：Obtained fromhttp://tools.iedb.org/main/datasets

  

### Model：Trained models

This folder contains trained models used by author to output results:

- Model(Five-fold cross-validation)： model trained on the proteins dataset using five-fold cross-validation.
- TlcMHCpan_model(BD2013)： model trained on the BD2013 dataset.
- TlcMHCpan_model：model trained on the proteins dataset.

### Notebooks

This folder contains code implementation of TlcMHCpan:

- Test Model: testing new data using the trained model.
- TlcMHCpan_model(BD2013):training the model on the BD2013 dataset.
- TlcMHCpan_model(Five-fold cross-validation):training the model using five-fold cross-validation.
- TlcMHCpan_model:training the model on the proteins dataset.
- Model_run_Benchmark(Benchmark data testing): testing benchmark datasets.

## Usage

#### Input file format

The input files are TXT files in the following format::

```
Peptide	HLA	BindingCategory
AAAAAAAALY	A*29:02	1
AAAAALQAK	A*03:01	1
AAAAALWL	C*16:01	1
AAAAARAAL	B*14:02	-1
AAAAEEEEE	A*02:01	-1
AAAAFEAAL	B*48:01	1
AAAAPYAGW	B*58:01	1
AAAARAAAL	B*14:02	1
AAAATCALV	A*02:01	1
......
```

#### Train

```python
 jupyter notebook-->TlcMHCpan_model
 
---train_data_path = '../data/proteins.txt'  # Path to the training data
---train_and_evaluate_model(train_data_path, model, loss_fn)  # Call the function to train and evaluate the model
```

The output will be like

```
Train Loss: 0.2840, Test Loss: 0.3402
Train ACC: 0.870, Test ACC: 0.857
Train AUC: 0.950, Test AUC: 0.933
Train Sensitivity: 0.813, Test Sensitivity: 0.808
Train Specificity: 0.919, Test Specificity: 0.900
Train F1: 0.853, Test F1: 0.839
Train SRCC: 0.778, Test SRCC: 0.839
```

#### Test

```python
jupyter notebook-->test model

model.load_state_dict(torch.load('../model/TlcMHCpan_model.pth'))  #Load the model
df_data= load_hla_dataframe('../data/sample_data.txt') #  Load the data
df_data= get_hla_subtype(df_data,)
evaluate_results = evaluate_module(model, df_data1) #Evaluate the results
```

The output will be like

```
{'Accuracy': 0.906, 'Sensitivity': 0.914, 'Specificity': 0.897, 'Threshold': 0.5, 'SRCC': 0.813, 'AUC': 0.969}
```



## Python and essential packages

```
python         3.10.9
numpy          1.23.5
pandas         1.5.3
torch       2.0.1+cu117
tensorflow     2.16.0
keras          3.3.3
```



