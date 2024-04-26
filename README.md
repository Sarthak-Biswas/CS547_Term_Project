
## Project Description  
This project aims to detect malware in PE (Portable Executable) files using Machine Learning techniques. We have developed a model that analyzes PE files and predicts whether they contain malware or not using hybrid static malware analysis(combination of PE Headers, byte-n-grams and opcode-n-grams features). This project can be a valuable tool in enhancing cybersecurity measures and protecting systems against malicious software/files.
   
## Dataset(s):  
1. PE files csv, containing metadata, header information [Dataset](https://www.kaggle.com/datasets/dasarijayanth/pe-header-data).  
2. byte and asm raw files, from kaggle microsoft malware classification challenge (BIG 2015) [Dataset](https://www.kaggle.com/competitions/malware-classification/data).  
   
## Preprocessing/Feature Extraction:  
  
### For Dataset-1:  
1. Dataset already has values for the features.  
2. Created a script to extract those features and header information from the given PE files like .exe, .dll file types.  
3. Used Extra-Trees classifier for the feature selection, important feature set from all the available information.  
  
### For Dataset-2:
1. Dataset has raw byte and asm files. Created seperate directories for each type and extracted file size as a feature for each file.  
2. Extracted N-grams from byte(byte-n-grams, where n= 1,2) and asm files(prefixes/keywords/registers/opcode-n-grams, where n= 1,2,3,4) as the features from each file.  
3. Converted asm files to image and extracted top performing 200 image pixels as features from that image.  
4. Used Random Forest for important features selection from all the above features separately for each feature set and merged them.  
  
Final dataset contains the following features.  
1. PE Header dataset  
2. Byte unigrams  
3. Opcode unigrams  
4. Top 300 Byte bigrams  
5. Top 200 Opcode bigrams  
6. Top 200 Opcode trigrams  
7. Top 200 Opcode tetragrams  
8. Top 200 Image Pixels  
   
## Training (build/train/evaluate)  
Trained various ML models on the above final dataset for the classification of files into malware/benign.  
Evaluation metrics used are accuracy, f1 score, confusion matrix.  
Random Forest model performed best among others like Gradient Boost, SVM.  

you can download the [trained Random Forest model](https://github.com/DasariJayanth/Malware-Detection-in-PE-files-using-Machine-Learning/blob/ce340fed1072ce4517e22c50d03e28b414bc3e87/models/RF_model.pkl) here.

## Setup  
  
Clone the repository to your local machine:

```
git clone https://github.com/DasariJayanth/Malware-Detection-in-PE-files-using-Machine-Learning.git  
```

Once you cloned the repository create a virtual environment using

```
python3 -m venv .venv
```

you might be required to set the policies to authorize the acivation of env    

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser  
```

Activate the environment:

```
source .venv/bin/activate
```

Next install the required libraries using:

```
pip install -r requirements.txt
```

Perform Feature extraction on your data as done in the `PE_Header(exe, dll files)/malware_test.py` and `Ngrams(byte, asm files)/N-grams.ipynb`. Also refer `Malware Detection Model.ipynb` for merging both feature sets before predicting with the model.    
  
Load the `models/RF_model.pkl` and run the loaded model on the extracted features for prediction.  
  
After you are done, Deactivate the virtual environment:  

```
deactivate  
```