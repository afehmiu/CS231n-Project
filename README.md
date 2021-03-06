# CS231n-Project
Implementing CNN Model for Covid-19 Detection using Chest X-Rays 

## Generating the Dataset 
1. Download the datasets listed below:
 * `git clone https://github.com/ieee8023/covid-chestxray-dataset.git`
 * `git clone https://github.com/agchung/Figure1-COVID-chestxray-dataset.git`
 * `git clone https://github.com/agchung/Actualmed-COVID-chestxray-dataset.git`
 * go to this [link](https://www.kaggle.com/tawsifurrahman/covid19-radiography-database) to download the COVID-19 Radiography database. Only the COVID-19 image folder and metadata file is required. The overlaps between covid-chestxray-dataset are handled
 * go to this [link](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge/data) to download the RSNA pneumonia dataset
2. Create a `data` directory and within the data directory, create a `train` and `test` directory
3. Use [create\_COVIDx\_v3.ipynb](create_COVIDx_v3.ipynb) to combine the three dataset to create COVIDx. Make sure to remember to change the file paths.
4. We provide the train and test txt files with patientId, image path and label (normal, pneumonia or COVID-19). The description for each file is explained below:
 * [train\_COVIDx3.txt](train_COVIDx3.txt): This file contains the samples used for training COVIDNet-CXR3.
 * [test\_COVIDx3.txt](test_COVIDx3.txt): This file contains the samples used for testing COVIDNet-CXR3.

## Downloading Pre-Trained Models
1. Download a model from the [pretrained models section]below:

|  Type | Input Resolution | COVID-19 Sensitivity | Accuracy | # Params (M) | MACs (G) |        Model        |
|:-----:|:----------------:|:--------------------:|:--------:|:------------:|:--------:|:-------------------:|
|  ckpt |      480x480     |         94.0         |   93.3   |      40.2    |  23.63   |[COVIDNet-CXR3-A](https://bit.ly/COVIDNet-CXR3-A)|
|  ckpt |      480x480     |         91.0         |   93.3   |      11.7    |   7.50   |[COVIDNet-CXR3-B](https://bit.ly/COVIDNet-CXR3-B)|
|  ckpt |      480x480     |         95.0         |   92.3   |       9.2    |   5.55   |[COVIDNet-CXR3-C](https://bit.ly/COVIDNet-CXR3-C)|
|  ckpt |      224x224     |   87.1 (on 31 test)  |   92.6   |     117.4    |   2.26   |[COVIDNet-CXR Small](https://bit.ly/CovidNet-CXR-Small)|
|  ckpt |      224x224     |   96.8 (on 31 test)  |   94.4   |     127.4    |   3.59   |[COVIDNet-CXR Large](https://bit.ly/CovidNet-CXR-Large)|

## Training and Testing the COVID-19 Net

### Training Steps 
TF training script from a pretrained model:
1. Use the tensorflow evaluation script, [train_tf.py](train_tf.py)
2. Locate the tensorflow checkpoint files (location of pretrained model)
3. To train from a pretrained model:
```
python train_tf.py \
    --weightspath models/COVIDNet-CXR3-B \
    --metaname model.meta \
    --ckptname model-1014
```
4. For more options and information, `python train_tf.py --help`

### Evaluation Steps 
1. Use the tensorflow evaluation script, [eval.py](eval.py)
2. Locate the tensorflow checkpoint files
3. To evaluate a tf checkpoint:
```
python eval.py \
    --weightspath models/COVIDNet-CXR3-B \
    --metaname model.meta \
    --ckptname model-1014
```
4. For more options and information, `python eval.py --help`


