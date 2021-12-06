
## Requirements

This project is implemented in Python using the [Tensorflow](https://www.tensorflow.org/) and [Keras](https://keras.io/) libraries to develop the model.

- OpenCV v4.4.0.46
- Ipython v7.16.1
- Keras v2.4.3
- Scikit-Image v0.17.2
- Scikit-Learn v0.24.2
- Tensorflow v2.5.1
- Livelossplot v0.5.3
- Matplotlib v3.3.2
- Numpy v1.19.2


### Install the repository:

```
git clone https://github.com/FernandoJRS/violence-detection-deeplearning
```

### Install the requirements:

```
pip install -r requirements.txt
```

## Model Architecture

The following graph shows the architecture of our model.

![Model Architecture](figures/ModelArchitecture.png?raw=True "Model Architecture")

In section A the architecture of the ViolenceNet model, that takes the optical flow as input, is shown. It is composed of four parts: a DenseNet-121 network spatio-temporal encoder, a multi-head self-attention layer, a bidirectional convolution 2D LSTM (BiConvLSTM2D) layer and a classifier. Below each Dense Block its number of components is indicated. The variable h corresponds to the number of heads used in parallel by the multi-head self-attention layer and the variables Q,K,V their inputs. Section B shows the internal architecture of a 5-component DenseBlock (x5).

## Results

This section shows the results obtained from the different experiments carried out with the datasets (HF - Hockey Fights), (MF - Movies Figths), (VF - Violent Flows) and (RLVS - Real Life Violence Situations).


### Ablation Study With Attention Mechanism, 5-Fold Cross-Validation

| Dataset |         Input        | Test Accuracy (with Attention) | Test Accuracy (without Att.) | Test Inference Time (with Attention) | Test Inference Time (without Att.) |
|---------|----------------------|--------------------------------|------------------------------|--------------------------------------|------------------------------------|
|   HF	  | Optical Flow         |         99.20 ± 0.6%	          |         99.00 ± 1.0%         |   0.1397 ± 0.0024 s                  |    0.1626 ± 0.0034 s               |
|   HF	  | Pseudo-Optical Flow  |         97.50 ± 1.0%	          |         97.20 ± 1.0%         |   0.1397 ± 0.0024 s                  |    0.1626 ± 0.0034 s               |
|   MF	  | Optical Flow         |         100.00 ± 0.0%	      |         100.00 ± 0.0%        |   0.1916 ± 0.0093 s                  |    0.2019 ± 0.0045 s               |
|   MF	  | Pseudo-Optical Flow  |         100.00 ± 0.0%	      |         100.00 ± 0.0%        |   0.1916 ± 0.0093 s                  |    0.2019 ± 0.0045 s               |
|   VF	  | Optical Flow         |         96.90 ± 0.5%	          |         94.00 ± 1.0%         |   0.2991 ± 0.0030 s                  |    0.3114 ± 0.0073 s               |
|   VF	  | Pseudo-Optical Flow  |         94.80 ± 0.5%	          |         92.50 ± 0.5%         |   0.2991 ± 0.0030 s                  |    0.3114 ± 0.0073 s               |
|  RLVS	  | Optical Flow         |         95.60 ± 0.6%	          |         93.40 ± 1.0%         |   0.2767 ± 0.020 s                   |    0.3019 ± 0.0059 s               |
|  RLVS	  | Pseudo-Optical Flow  |         94.10 ± 0.8%	          |         92.20 ± 0.8%         |   0.2767 ± 0.020 s                   |    0.3019 ± 0.0059 s               |

### Performance Comparison For One Iteration

| Dataset |         Input        | Training Accuracy | Training Loss | Test Accuracy Violence | Test Accuracy Non-Violence | Test Accuracy |
|---------|----------------------|-------------------|---------------|------------------------|----------------------------|---------------|
|  HF	  | Optical Flow         |  100%             |  1.20×10−5    |  99.00%                |  100.00%                   |  99.50%       |
|  HF	  | Pseudo-Optical Flow  |  99%              |  1.35×10−5    |  97.00%                |  98.00%                    |  97.50%       |
|  MF	  | Optical Flow         |  100%             |  1.18×10−5    |  100%                  |  100%                      |  100%         |
|  MF	  | Pseudo-Optical Flow  |  100%             |  1.19×10−5    |  100%                  |  100%                      |  100%         |
|  VF	  | Optical Flow         |  98%              |  1.50×10−4    |  97.00%                |  96.00%                    |  96.50%       |
|  VF	  | Pseudo-Optical Flow  |  97%              |  2.94×10−4    |  95.00%                |  94.00%                    |  94.50%       |
|  RLVS	  | Optical Flow         |  97%              |  3.10×10−4    |  96.00%                |  95.00%                    |  95.50%       |
|  RLVS	  | Pseudo-Optical Flow  |  95%              |  7.31×10−4    |  94.00%                |  93.00%                    |  93.50%       |

### Cross-Dataset Experiment, 5-Fold Cross-Validation

| Dataset Training | Dataset Testing | Test Accuracy Optical Flow | Test Accuracy Pseudo-Optical Flow |
|------------------|-----------------|----------------------------|-----------------------------------|
|  HF	           | MF              |  65.18 ± 0.34%             |  64.86 ± 0.41%                    |
|  HF	           | VF              |  62.56 ± 0.33%             |  61.22 ± 0.22%                    |
|  HF	           | RLVS            |  58.22 ± 0.24%             |  57.36 ± 0.22%                    |
|  MF	           | HF              |  54.92 ± 0.33%             |  53.50 ± 0.12%                    |
|  MF	           | VF              |  52.32 ± 0.34%             |  51.77 ± 0.30%                    |
|  MF	           | RLVS            |  56.72 ± 0.19%             |  55.80 ± 0.20%                    |
|  VF	           | HF              |  65.16 ± 0.59%             |  64.76 ± 0.49%                    |
|  VF	           | MF              |  60.02 ± 0.24%             |  59.48 ± 0.16%                    |
|  VF	           | RLVS            |  58.76 ± 0.49%             |  58.32 ± 0.27%                    |
|  RLVS	           | HF              |  69.24 ± 0.27%             |  68.86 ± 0.14%                    |
|  RLVS	           | MF              |  75.82 ± 0.17%             |  74.64 ± 0.22%                    |
|  RLVS	           | VF              |  67.84 ± 0.32%             |  66.68 ± 0.22%                    |
|  HF + MF + VF	   | RLVS            |  70.08 ± 0.19%             |  69.84 ± 0.14%                    |
|  HF + MF + RLVS  | VF              |  76.00 ± 0.20%             |  75.68 ± 0.14%                    |
|  HF + RLVS + VF  | MF              |  81.51 ± 0.09%             |  80.49 ± 0.05%                    |
|  RLVS + MF + VF  | HF              |  79.87 ± 0.33%             |  78.63 ± 0.01%                    |


## Evaluation

We provide a [Jupyter Notebook](ViolenceActionDetection.ipynb) with instructions to train and test our model.

In order to run the application it is necessary to download the datasets. And to download the datasets it is necessary to upload the kaggle.json file found in this repository.

The following steps must be followed:

1. First step

    Download the kaggle.json file to a local environment

2. Second step

    Open the [Jupyter Notebook](ViolenceActionDetection.ipynb)

3. Third step

    Execute the first cell of the jupyter notebook.

4. Step four

    After executing the first cell, it will ask you to load the kaggle.json file. Do it.

5. Fifth step

    After the datasets is downloaded, run the other parts of the code.



