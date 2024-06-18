# OCR-arabic
ocr system for arabic manuscript using CRNN+CTC architecture    
Based on the code snippet you provided, it appears that the data sequencing strategy is as follows:

1. The `sets` list includes four sets: `set_a`, `set_b`, `set_c`, and `set_d`.
2. The code constructs a list of image file paths for each set by searching for `.tif` files within the respective directories.
3. The data is then split into training and testing sets:
    - Files from `set_d` are added to the `test_data`.
    - Files from the other sets (`set_a`, `set_b`, and `set_c`) are added to the `train_data`.

This means that the model was trained on images from `set_a`, `set_b`, and `set_c`, and then evaluated on images from `set_d`.

### Updated README with Sequencing Explanation

## Arabic OCR Manuscript System Using CRNN and CTC Architecture

This project implements an Arabic OCR (Optical Character Recognition) manuscript system using a CRNN (Convolutional Recurrent Neural Network) and CTC (Connectionist Temporal Classification) architecture.

### Overview

The system is designed to recognize handwritten Arabic text. It combines CNNs for feature extraction, RNNs for sequence modeling, and CTC for aligning predicted sequences with actual text.

### Model Architecture

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

### Dataset

The IFN/ENIT database is the most widely used and popular database for handwritten Arabic text recognition research, published by Pechwitz and Maergner. It consists of 1,000 forms written by 411 distinct writers, divided into five training and testing groups. The database includes approximately 27,000 handwritten Arabic names representing Tunisian city names, with a lexicon size of 937 place names. Each word in the database has a corresponding Ground Truth (GT) file containing information such as the baseline position and individual characters used.

![IFN/ENIT Database Samples](path/to/your/image.png)

### Sequencing of Data

The dataset was split into training and testing sets based on the following strategy:

1. **Sets Included**: `set_a`, `set_b`, `set_c`, and `set_d`.
2. **File Path Extraction**: The code searches for `.tif` files within each set's directory.
3. **Training Set**: Includes images from `set_a`, `set_b`, and `set_c`.
4. **Testing Set**: Includes images from `set_d`.

This approach ensures that the model is trained on a diverse set of examples and evaluated on a separate set to test its generalization performance.

###  Division of Sets

1.** Data Paths and Ground Truth Files:**   

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

\[ CAR = \left(1 - \frac{S + I + D}{N}\right) \times 100 \]

Where:
- \( S \) is the total number of substituted characters.
- \( I \) is the total number of inserted characters.
- \( D \) is the total number of deleted characters.
- \( N \) is the total number of characters in the evaluation set.

### Training Details

- **Epochs**: 20
- **Best Validation Loss**: 10.9893 at epoch 19

### Installation and Usage

To use this OCR system, follow these steps:

1. Clone the repository.
2. Install the required dependencies.
3. Prepare your dataset in the specified format.
4. Train the model using the provided training script.
5. Use the trained model to recognize text from handwritten Arabic manuscript images.

### Conclusion

This OCR system leverages the strengths of CNNs, RNNs, and CTC to accurately recognize and interpret handwritten Arabic text, providing a robust solution for Arabic manuscript digitization.

---

### Acknowledgments

This project is built upon the foundational concepts of deep learning and OCR, utilizing CNNs, RNNs, and CTC for a comprehensive text recognition system.

---

By understanding and using this architecture, developers and researchers can build effective OCR systems for various handwritten text recognition tasks.



