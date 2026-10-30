# PHISHING-URL-DETECTION-USING-CHARACTERLEVEL-LSTM-NEURAL-NETWORKS
DL_PROJECT_PHISHING URL DETECTION USING CHARACTERLEVEL LSTM NEURAL NETWORKS


##  Project Overview

Phishing is a cyberattack in which attackers create deceptive URLs and websites to trick users into revealing sensitive information such as passwords, banking details, and personal data.

**Phishing URL Detection Using Character-Level LSTM Neural Networks** is a deep learning project that classifies URLs as either **Legitimate or Phishing** using a Long Short-Term Memory (LSTM) neural network.

The project uses the **PhiUSIIL Phishing URL Dataset** from the UCI Machine Learning Repository. Instead of relying on manually extracted URL features, the model processes URLs character by character and learns patterns that help distinguish legitimate URLs from potentially malicious ones.

The trained model also estimates the probability that a given URL is associated with phishing.

## Objectives

* Develop an automated phishing URL detection system using deep learning.
* Process and analyze URL data from the PhiUSIIL dataset.
* Convert URL characters into numerical sequences.
* Build and train a character-level LSTM neural network.
* Evaluate the model using multiple classification metrics.
* Predict whether a user-provided URL is legitimate or phishing.
* Estimate the phishing probability for a given URL.

## Features

* **Character-Level Processing:** Converts URL characters into numerical representations.
* **Deep Learning:** Uses an LSTM network to learn sequential patterns in URLs.
* **Data Preprocessing:** Cleans URL data and standardizes URL sequences to 200 characters.
* **Binary Classification:** Classifies URLs as legitimate or phishing.
* **Performance Evaluation:** Calculates accuracy, precision, recall, F1-score, and ROC-AUC.
* **Confusion Matrix:** Visualizes correct and incorrect classifications.
* **ROC Curve:** Evaluates the model's ability to distinguish between the two classes.
* **URL Prediction:** Accepts a new URL and returns its predicted class and estimated phishing probability.
* **Model Saving:** Saves the trained model and preprocessing configuration for future use.

## Technologies Used

| Technology                      | Purpose                                 |
| ------------------------------- | --------------------------------------- |
| Python                          | Programming language                    |
| Google Colab                    | Development and execution environment   |
| TensorFlow                      | Deep learning framework                 |
| Keras                           | LSTM model implementation               |
| NumPy                           | Numerical operations                    |
| Pandas                          | Dataset processing                      |
| Scikit-learn                    | Data splitting and evaluation metrics   |
| Matplotlib                      | Visualization                           |
| Seaborn                         | Confusion matrix and data visualization |
| UCI Machine Learning Repository | Dataset source                          |

##  Dataset

**Dataset Name:** PhiUSIIL Phishing URL Dataset

**Source:** UCI Machine Learning Repository

**Dataset Link:** https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset

The dataset contains URL-related information and corresponding class labels. The implementation extracts the URL and label columns and prepares them for binary classification.

### Class Labels

| Label | Class      |
| ----- | ---------- |
| 0     | Legitimate |
| 1     | Phishing   |

The notebook removes records with missing or empty URLs, cleans the data, and converts the URLs into numerical character sequences.

To keep training manageable, the notebook limits the dataset to a maximum of 100,000 records when necessary.

## Methodology

The project follows these steps:

1. **Dataset Loading:** Load the PhiUSIIL dataset from the UCI Machine Learning Repository.
2. **Data Extraction:** Extract URLs and their corresponding labels.
3. **Data Cleaning:** Remove missing values, empty URLs, and unnecessary surrounding whitespace.
4. **Character Encoding:** Assign numerical IDs to individual URL characters.
5. **Sequence Preparation:** Pad or truncate each URL to a fixed length of 200 characters.
6. **Dataset Splitting:** Divide the data into training, validation, and testing sets.
7. **Model Construction:** Build a character-level LSTM neural network.
8. **Model Training:** Train the network using the Adam optimizer and binary cross-entropy loss.
9. **Model Evaluation:** Calculate performance metrics and generate a confusion matrix and ROC curve.
10. **URL Prediction:** Accept a new URL and predict its class and estimated phishing probability.
11. **Model Saving:** Save the trained model, character vocabulary, and preprocessing configuration.

### Dataset Splitting

The dataset is divided into three subsets:

| Dataset        | Percentage | Purpose                                   |
| -------------- | ---------: | ----------------------------------------- |
| Training Set   |        80% | Train the model                           |
| Validation Set |        10% | Monitor training performance              |
| Testing Set    |        10% | Evaluate the trained model on unseen data |

Stratified splitting is used to preserve the class proportions as closely as possible.

##  LSTM Model Architecture

The proposed model uses the following architecture:

| Layer            | Configuration                | Purpose                                       |
| ---------------- | ---------------------------- | --------------------------------------------- |
| Input Layer      | 200 character IDs            | Accepts encoded URLs                          |
| Embedding Layer  | 32 dimensions                | Converts character IDs into learnable vectors |
| SpatialDropout1D | 0.2 dropout rate             | Helps reduce overfitting                      |
| LSTM Layer       | 64 units, dropout 0.2        | Learns sequential character patterns          |
| Dense Layer      | 32 neurons, ReLU activation  | Learns additional patterns                    |
| Dropout Layer    | 0.3 dropout rate             | Reduces reliance on individual activations    |
| Output Layer     | 1 neuron, Sigmoid activation | Produces the estimated phishing probability   |

### Model Configuration

* **Optimizer:** Adam
* **Loss Function:** Binary Cross-Entropy
* **Maximum Epochs:** 10
* **Batch Size:** 128
* **Classification Threshold:** 0.5
* **Early Stopping:** Monitors validation loss and restores the best model weights.
* **Learning Rate Scheduling:** Reduces the learning rate when validation loss stops improving.

The sigmoid output produces a value between 0 and 1. A value greater than or equal to 0.5 is classified as phishing; a value below 0.5 is classified as legitimate.

##  Model Evaluation Results

The trained LSTM model achieved the following results on the test dataset.

| Evaluation Metric |   Score |
| ----------------- | ------: |
| Accuracy          |  99.88% |
| Precision         | 100.00% |
| Recall            |  99.72% |
| F1-Score          |  0.9986 |
| ROC-AUC           |  0.9991 |

### Confusion Matrix Results

| Actual Class | Predicted Legitimate | Predicted Phishing |
| ------------ | -------------------: | -----------------: |
| Legitimate   |                5,730 |                  0 |
| Phishing     |                   12 |              4,258 |

### Interpretation

* **True Negatives (5,730):** Legitimate URLs correctly classified as legitimate.
* **False Positives (0):** Legitimate URLs incorrectly classified as phishing.
* **False Negatives (12):** Phishing URLs incorrectly classified as legitimate.
* **True Positives (4,258):** Phishing URLs correctly classified as phishing.

### Result Analysis

The model achieved an accuracy of **99.88%** and a precision of **100.00%** on the reported test set. Its recall of **99.72%** indicates that it correctly identified nearly all phishing URLs in that test set.

The ROC-AUC score of **0.9991** indicates excellent discrimination between the two classes on the evaluated data.

These results demonstrate strong performance on the test dataset. However, further testing on recent and independently collected URLs is necessary to determine how well the model generalizes to real-world phishing attacks.

## URL Prediction

The project includes a prediction function that accepts a URL and returns its predicted class and estimated phishing probability.

### Example

```python
result = predict_url("https://example.com/login")

print("URL:", result["url"])
print("Prediction:", result["prediction"])
print("Phishing Probability:", result["phishing_percentage"], "%")
```

### Prediction Output

The model returns the following information:

* **URL:** The URL provided by the user.
* **Prediction:** `LEGITIMATE` or `PHISHING`.
* **Phishing Probability:** The model's estimated phishing probability expressed as a percentage.
* **Classification Threshold:** 0.5.

The prediction function uses the same character encoding, padding, and truncation process applied during training.

**Note:** The example URL is illustrative. Its actual prediction and probability depend on the trained model.

##  Visualizations

The notebook generates visualizations to help understand the dataset and evaluate model performance, including:

* Distribution of legitimate and phishing URLs.
* URL length distribution by class.
* Training and validation accuracy.
* Training and validation loss.
* Confusion matrix heatmap.
* Receiver Operating Characteristic (ROC) curve.

These visualizations help analyze model performance and identify potential classification errors.

##  How to Run the Project

The project can be executed using Google Colab.

### Step 1: Open the Notebook

Open `DL_Pro.ipynb` in Google Colab.

### Step 2: Install Dependencies

Run the following command in a notebook cell if the required packages are not already installed:

```python
!pip install ucimlrepo tensorflow numpy pandas matplotlib seaborn scikit-learn
```

### Step 3: Execute the Notebook

Run the notebook cells in order.

The notebook will:

1. Import the required libraries.
2. Download the PhiUSIIL dataset.
3. Clean and preprocess the data.
4. Encode URLs into numerical sequences.
5. Split the dataset.
6. Build and train the LSTM model.
7. Evaluate the model and generate visualizations.
8. Allow URL prediction.
9. Save the trained model and preprocessing files.

### Step 4: Test a URL

Execute the URL prediction cell and enter a URL when prompted.

The model will display the predicted class and estimated phishing probability.

### Step 5: Save the Model

The notebook saves the trained model and preprocessing files in the `phishing_lstm_project` directory and creates a ZIP archive for download.

## Saved Model Files

After successful execution, the notebook generates the following files:

```text
phishing_lstm_project/
├── phishing_lstm_model.keras
├── character_vocabulary.json
└── model_config.json
```

* `phishing_lstm_model.keras` — Contains the trained LSTM model.
* `character_vocabulary.json` — Stores the character-to-ID mapping.
* `model_config.json` — Stores preprocessing settings and the classification threshold.

These files can be used to load the trained model and perform predictions without retraining it, provided the required dependencies and compatible preprocessing configuration are available.

##  Advantages

* Learns URL character patterns directly from data.
* Reduces dependence on manually engineered URL features.
* Supports binary classification of legitimate and phishing URLs.
* Provides an estimated phishing probability.
* Uses validation data and early stopping during training.
* Evaluates performance using multiple complementary metrics.
* Supports saving and reusing the trained model.

##  Limitations

* The model may produce false-positive and false-negative predictions.
* Performance depends on the quality and diversity of the training dataset.
* URLs longer than 200 characters are truncated.
* The model analyzes URL text and does not inspect webpage content, domain registration information, certificates, or live website behavior.
* Performance may differ on newly emerging phishing patterns and URLs from other sources.
* The estimated phishing probability is not necessarily a calibrated measure of real-world risk.
* The model should not be used as the sole basis for deciding whether a website is safe.

##  Future Enhancements

Potential improvements include:

* Developing a web application for URL checking.
* Integrating the model into a browser extension.
* Training and testing on larger and more recent datasets.
* Comparing LSTM performance with CNN, GRU, and traditional machine learning models.
* Combining character-level analysis with domain information and URL lexical features.
* Optimizing the model for faster predictions.
* Improving explainability to identify URL patterns that influence predictions.
* Integrating the model into email filtering or broader security workflows.

These are proposed enhancements; the current notebook implements model training, evaluation, URL prediction, and model saving.

##  Project Team

**Institution:** Prasad V. Potluri Siddhartha Institute of Technology

**Department:** Computer Science and Engineering

**Academic Year:** 2026–2027

**Course:** Deep Learning

**Faculty Guide:** Dr. G. Lalitha Kumari

### Team Members

1. Mandadhi Janani
2. Mukku Dakshayani
3. Muddineni Yamini

##  References

1. UCI Machine Learning Repository — [PhiUSIIL Phishing URL Dataset](https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset)
2. [TensorFlow Documentation](https://www.tensorflow.org/)
3. [Keras Documentation](https://keras.io/)
4. [Scikit-learn Documentation](https://scikit-learn.org/)

##  Conclusion

This project demonstrates the application of deep learning to phishing URL detection using a character-level LSTM neural network.

By converting URL characters into numerical sequences and learning their sequential patterns, the model distinguishes between legitimate and phishing URLs. The reported test results show an accuracy of 99.88% and an ROC-AUC of 0.9991.

The project provides a foundation for further research and development in automated phishing detection. Additional testing on diverse, recent, and independent datasets would help assess its reliability in real-world cybersecurity applications.

---

**Disclaimer:** This project is developed for educational and research purposes. Model predictions are estimates and do not guarantee that a URL is safe or malicious. Always verify suspicious links using appropriate security tools and trusted sources.
