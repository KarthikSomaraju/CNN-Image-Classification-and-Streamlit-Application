# CNN Image Classification and Streamlit Application

**Author:** Karthik Somaraju

**Dataset:** MNIST (handwritten digits 0 to 9)

**Streamlit app topic:** Student Marks Calculator

## Overview
This project has two parts:

- **Part A - CNN image classification:** a Convolutional Neural Network that looks at a 28 x 28 grayscale image of a handwritten digit and predicts which digit (0 to 9) it is.
- **Part B - Streamlit application:** a simple web app that calculates a student's result from the marks of five subjects.

## Part A - CNN (MNIST)

### Dataset
- 70,000 grayscale images, 28 x 28 pixels
- 60,000 training images and 10,000 test images
- 10 classes (digits 0 to 9), roughly balanced
- Loaded directly from Keras, so no download or upload is needed

### Workflow
1. Load the data and check shapes, classes and sample count
2. Check the class distribution and view sample images
3. Preprocess: normalize pixels to 0-1 and add the channel dimension (28, 28, 1)
4. Keep labels as integers (no one-hot encoding needed)
5. Build, compile and train the CNN (5 epochs, 10% validation split)
6. Evaluate on the test data
7. Compare actual vs predicted labels and look at the wrong predictions

### Model architecture
| Layer | Output shape | Parameters |
|---|---|---|
| Conv2D (32 filters, 3x3, ReLU) | (26, 26, 32) | 320 |
| MaxPooling2D (2x2) | (13, 13, 32) | 0 |
| Flatten | (5408) | 0 |
| Dense (64, ReLU) | (64) | 346,176 |
| Dense (10, softmax) | (10) | 650 |
| **Total** | | **347,146** |

Compiled with the Adam optimizer, `sparse_categorical_crossentropy` loss and accuracy as the metric.

### Results
| Metric | Value |
|---|---|
| Test accuracy | 97.94% (9,794 of 10,000 correct) |
| Test loss | 0.0683 |
| Final training accuracy | 99.44% |
| Final validation accuracy | 98.12% |

Validation loss starts to rise after epoch 3 while training loss keeps falling, which shows mild overfitting. Most wrong predictions are unclear or unusual handwriting.

## Part B - Streamlit app: Student Marks Calculator

**Inputs:** student name and marks (out of 100) for Mathematics, Science, English, Social Studies and Computer Science.

**Processing:**
- Total = sum of the five marks
- Percentage = total / 500 x 100
- Grade: A+ (90 and above), A (80-89), B (70-79), C (60-69), D (50-59), F (below 50)
- A subject is failed if the marks are below 35

**Outputs:** total, percentage and grade, a PASS / FAIL message listing subjects that need improvement, and a bar chart of the marks.

**Invalid input handling:** an empty name, a name with digits or symbols, and all marks being 0 show an error or warning message. The marks box only accepts whole numbers from 0 to 100.

## How to run

1. Install the requirements:
   ```
   pip install tensorflow numpy matplotlib streamlit pandas
   ```
2. Run the CNN part (Part A) as a Python script or notebook to train and evaluate the model.
3. Run the Streamlit app (Part B):
   ```
   streamlit run app.py
   ```
## Technologies used
Python, TensorFlow / Keras, NumPy, Matplotlib, Pandas, Streamlit

## Google Collab Link
https://colab.research.google.com/drive/1TCKdA-5AzTiL01DLafqiQNU4GfGQqMxQ?usp=sharing
