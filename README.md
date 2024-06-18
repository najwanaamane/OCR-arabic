

## Arabic OCR Manuscript System Using CRNN and CTC Architecture

This project implements an Arabic OCR (Optical Character Recognition) manuscript system using a CRNN (Convolutional Recurrent Neural Network) and CTC (Connectionist Temporal Classification) architecture.

### Overview

The system is designed to recognize handwritten Arabic text. It combines CNNs for feature extraction, RNNs (LSTM) for sequence modeling, and CTC for aligning predicted sequences with actual text.

### Model Architecture   

![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/e0d500c4-bcb9-4b6c-bb92-e151d6977ccd)   




#### CNN for Feature Extraction

- **Local Feature Detection**: Detects patterns like edges and textures.
- **Hierarchical Learning**: Learns from simple to complex features.
- **Translation Invariance**: Handles variations in handwriting.

#### RNN (LSTM) for Sequence Modeling

- **Temporal Dependencies**: Understands the sequence context of characters.
- **Sequence Prediction**: Outputs probabilities for each character in the sequence.
- **Context Awareness**: Learns long-term dependencies in text sequences.

#### CTC for Sequence Alignment

- **Flexible Alignment**: Aligns input data with output labels without pre-segmentation.
- **Handles Variable Lengths**: Manages sequences of different lengths.
- **CTC Blank Token**: Improves alignment and accuracy by allowing the network to output a blank token for better sequence handling.

  
 ![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/5e6fcd80-ad41-4a72-b4b5-c987d681de21)   




### Dataset

The IFN/ENIT database is the most widely used and popular database for handwritten Arabic text recognition research, published by Pechwitz and Maergner. It consists of 1,000 forms written by 411 distinct writers, divided into five training and testing groups. The database includes approximately 27,000 handwritten Arabic names representing Tunisian city names, with a lexicon size of 937 place names. Each word in the database has a corresponding Ground Truth (GT) file containing information such as the baseline position and individual characters used.   


**IFN/ENIT Database Samples**    
![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/3fd62982-faf4-43b8-a059-04d8429634d7)


### Sequencing of Data

The dataset was split into training and testing sets based on the following strategy:

1. **Sets Included**: `set_a`, `set_b`, `set_c`, and `set_d`.
2. **File Path Extraction**: The code searches for `.tif` files within each set's directory.
3. **Training Set**: Includes images from `set_a`, `set_b`, and `set_c`.
4. **Testing Set**: Includes images from `set_d`.

This approach ensures that the model is trained on a diverse set of examples and evaluated on a separate set to test its generalization performance.   

### Training Details

- **Epochs**: 20
- **Loss Function**: CTC Loss; specifically designed for sequence labeling tasks, it helps the model learn to predict the most likely character sequences for the input images by penalizing deviations from the ground truth while accounting for potential variations in sequence lengths.

- **Best Validation Loss**: 10.9893 at epoch 19   

  ![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/001b4a87-d662-4f0e-8f62-f5e2c57fc744)



 #### Additional Techniques: Beam Search and Mapping
-**Beam Search**: Implemented to enhance sequence decoding, providing a more refined approach to predicting sequences.  

![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/4bb79267-9822-4f14-a9de-f54c81fabc92)



![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/7197e97b-e0cd-4eba-aa6b-8411640211f9)


-**Sequence Mapping**: After prediction using beam search, sequences are mapped to actual Arabic words using a character mapping technique.   

![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/97264573-decc-45a6-883a-fff185f18492)


![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/a8314d96-f7d1-461c-ad50-c2beac7114e6)


###  Division of Sets and Testing

1.**Data Paths and Ground Truth Files:**   

The paths to the images and ground truth files are defined at the beginning.
true variable holds the path to a specific .tru file.
racine_gt is the root path for ground truth files.

2.**Fetching Ground Truth:**   

The get_Word function reads the ground truth text from the .tru files. It extracts the relevant word from the sixth line of the file.     

3.**Preprocessing and Prediction:**      

preprocess_image function preprocesses the images to the required format.   
decode_prediction decodes the model predictions into readable text using a character mapping.    

4.**Inference Model:**   

The inference model is created using the trained model's input and output layers.   

5.**Testing and Evaluation:**    

Multiple tests are run with different image paths (e.g., set_a, set_d).   
Ground truth and predicted texts are mapped and printed.   

### Results

| Metric                         | Value                   |
|-------------------------------|-------------------------|
| Character Accuracy Rate (CAR) for set_d | 0.3094783068352783   |
| Character Accuracy Rate (CAR) for set_a | 0.49808497056528833  |
| Validation Loss for set_e      | 23.480015925357215      |
| Validation Loss for set_d      | 11.24458679163231       |

#### Character Accuracy Rate (CAR)

Character Accuracy Rate (CAR) is the percentage of characters that have been correctly recognized in all words. It is usually measured using the edit distance method and is defined as the minimum number of insertions, deletions, or substitutions of a single terminal needed to transform one string into the other.   

![image](https://github.com/najwanaamane/OCR-arabic/assets/86806375/a2a72ebf-1eda-4d9d-9b1d-80b6b873a6e7)

Where:
- \( S \) is the total number of substituted characters.
- \( I \) is the total number of inserted characters.
- \( D \) is the total number of deleted characters.
- \( N \) is the total number of characters in the evaluation set.


### Installation and Usage

To use this OCR system, follow these steps:

1. Clone the repository.
2

