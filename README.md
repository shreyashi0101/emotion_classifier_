Description
This project builds a complete machine learning pipeline that classifies emotional states from audio clips using speech and song recordings. Audio features like MFCCs, Chroma, and Spectrograms were extracted and used to train a classifier. The final model—a Random Forest Classifier—was tuned to achieve high accuracy and deployed as a Streamlit web app.

Dataset

We used two datasets:

Audio_Speech_Actors_01-24: Contains speech audio files.

Audio_Song_Actors_01-24: Contains sung audio .

Each audio filename encodes metadata, including emotion type, which was mapped as:

emotion_map = {
'01': 'neutral',
'02': 'calm',
'03': 'happy',
'04': 'sad'
'05': 'angry',
'06': 'fearful',
'07': 'disgust',
'08': 'surprised'
}

Preprocessing & Feature Extraction

Feature Extraction:
We extracted the following features using librosa:

MFCC (Mel Frequency Cepstral Coefficients): 40 coefficients averaged over time.

Chroma STFT

Mel Spectrogram

Spectral Contrast

Ton

Each audio file was transformed into a fixed-length feature vector (approximately 40–100 features depending on configuration).

Data Cleaning:

Removed corrupted files or feature extraction failures.

Ensured all samples had consistent length and features.

Label Encoding:

Used LabelEncoder to convert string labels (e.g., "happy") to integers.

Saved using joblib for reuse in prediction.

Train-Test Split:

Combined both speech and song data after feature extraction.

Final dataset shape: (2452, 41) → 40 features + 1 label.

Used an 80/20 split for training and testing.

Stratified sampling was applied to preserve emotion distribution.

Model Pipeline

Be

Best Hyperparameters:
{
'bootstrap': False,
'
'min_samples_leaf': 1,
'me
'n_es_
}

Evaluation Metrics

Accuracy Results:
Cross-Validation Accuracy: 0.7563
Test Accuracy: 0.7658

Classification Report:
Emotion Precision Recall F1-score Support
Anger
Calm
Discus
Fearful 0.76 0.69 0.73 75
H
Neutral 0.93 0.74 0.82 38
S
Surp

Overall F1 Score: 0.77

Feature Importance:
A bar graph was plotted to visualize the top MFCC features contributing to prediction, showing mfcc_1, mfcc_3, mfcc_5, etc., as most influential.

Cross Validation:

Applied 5-Fold Cross Validation.

Average CV Accuracy: 0.70+

Validated that model generalizes well across different splits.

Streamlit Web App:

Built using Streamlit and deployed on Streamlit Cloud.

Upload any .wav file and the app predicts the emotion.

Uses trained model.pkl and label_encoder.pkl.

Project Structure:

emotion_classifier_project/
├── data/
│ ├── Audio_Speech_Actors_01-24/
│ └── Audio_Song_Actors_01-24/
├── app/
│       app.py
├── train_model.ipynb (Full training pipeline)
├── test.py (Predicts emotion from audio file)
├── model.pkl
├── label_encoder.pkl (Label encoder for decoding predictions)
├── requirements.txt (All dependencies)
└── README.md (Project documentation)

Future Improvements:


Apply data augmentation: pitch shifting, background noise, etc.

Use ensemble methods for better generalization.

Use transfer learning with spectrogram images (e.g., ResNet).

Address underperforming classes (like "disgust" and "surprised").

License:
This project is created for academic and educational purposes.
Made with love by Shreyashi 
