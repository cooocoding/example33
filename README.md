# Classification of  Upper Gastrointestinal Submucosal Lesions Using Multimodal Data Fusion Strategy

## Introduction
This is a final year project of Macau University of Science and Technology. The project improves on the basis of the single-modal ViT model and proposes the MMViT model, a new method for identifying submucosal lesions of the upper gastrointestinal tract using a multi-modal model. Our model achieved an accuracy rate of 65.33% on 603 sample data calculations, improving the recognition accuracy rate of the original single-modal ViT model.  
For more related information, please refer to materials `Thesis(Final).ChenRui.2023-5-14.pdf`.
## File composition
* `data_process.ipynb`: Preprocessing of dataset images.
* `counting.ipynb`: Count the number of images of each lesion in the training set/test set.
* `dataset.py`: Load and preprocess data for MMViT models.
* `make_json1.py`: Read a list of paths that generate lesion images.
* `train.py`: Train, test, and evaluate models.
* `vit.py`: Implementation of the ViT model.
* `roc.py`: Draw three types of ROC curve and AUC score.
* `plot.ipynb`: Draw single-modal model and multi-modal model Acc and Loss curve comparison.
* `roc.ipynb`: Draw single-modal model and multi-modal model ROC curve and AUC score comparison.   
<br> 
Among them, the `test0` folder is the realization of the single-modal ViT model, and the `test1` folder is the realization of the multi-modal MMViT model. The file structure in the folder is the same, unprocessed training set data is stored in `dataset2`, unprocessed test set data is stored in `test_data2`, processed training set data is stored in `train`, and processed test set data is stored in `test`.

## Requirements & Dependencies

The experimental environment of this project is based on the `Ubuntu (18.04.3 LTS)` system and the `Nvidia Tesla V100 GPU` with 32GB of memory. The deep learning framework `PyTorch` and `Python 3.8` are used to complete the image processing and model training required for the project.
* `torch` 1.10.2
* `torchvision` 0.11.3
* `einops version` 0.4.0
* `torchsummary` 1.5.1
* `sklearn` 0.22
* `matplotlib` 3.11
* `numpy` 1.17.3

> Note: The bundled `venv` in the repository should contain all dependencies that this project requires.  

## Usage
### Step 1: Generate train set and test set
Run `data_preprocess.ipynb`, the file will preprocesses the images. The training set and test set are stored in the train and test folders respectively.

### Step 2: Generate JSON files

Run `make_json1.py` to generate the json file of the image path, generate `trian.json` and `test.json` for model training and test reading.

### Step 3: Train and test the model

Run `train.py`,`-l` specifies the learning rate, `-e` specifies the number of epochs. For example,
```
python train.py -l 1e-3 -e 200
```

### Step 4: Plot
**Accuracy curve, loss curve, confusion matrix**  
After running `train.py`, the _accuracy curve_, _loss curve_ and _confusion matrix_ will be generated.  
<br>
In addition, `accuracy.txt` and `loss.txt` will be generated.   
* Put the two txt files obtained by using only endoscopic images of the single-modal ViT model in the `ING` folder   
* Place the two txt files obtained by using only the endoscopic ultrasound images of the single-modal ViT model in the `EUS` folder   
* Put the two txt files obtained from the multimodal ViT model in the `EUS+ING` folder  
* Run `plot.ipynb` to generate the accuracy curve and loss curve that combine the three into one graph.    
  

**ROC curve and AUC score**  
After running `train.py`, if we choose to calculate micro avg AUC, the additional `micro_fpr.txt` and `micro_tpr.txt` will be generated.  
* Put the two txt files obtained by using only endoscopic images of the single-modal ViT model in the `ING` folder
* Place the two txt files obtained by using only the endoscopic ultrasound images of the single-modal ViT model in the `EUS` folder 
* Put the two txt files obtained from the multimodal ViT model in the `EUS+ING` folder 
* Run `roc.ipynb` to generate the ROC curve and AUC score that combine the three into one graph.

