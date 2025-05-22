## 🫀 MIT-BIH ECG Preprocessing Project

Welcome to my ECG signal preprocessing project using the MIT-BIH Arrhythmia dataset.  
This repo focuses on preparing ECG signals for analysis or deep learning by applying filtering, normalization, and noise handling techniques. 🎯

---

## 📦 Dataset Info

- 📁 Source: [Kaggle - MIT-BIH Arrhythmia (2023)](https://www.kaggle.com/datasets/protobioengineering/mit-bih-arrhythmia-database-modern-2023)
- 🧾 Format: `.csv` files, each containing raw ECG data from a patient record
- ⚙️ Sampling Rate: 360 Hz (standard)

---

## 🧠 Preprocessing Steps

## ✅ 1. Bandpass Filtering  

def bandpass_filter(signal, lowcut=0.5, highcut=45.0, fs=360, order=4):
    nyquist = 0.5 * fs
    low = lowcut / nyquist
    high = highcut / nyquist
    b, a = butter(order, [low, high], btype="band")
    return filtfilt(b, a, signal)

---

## ✅ 2. Normalization
Standardizes the ECG signal to have zero mean and unit variance:

python:
def normalize_signal(signal):
    return (signal - np.mean(signal)) / np.std(signal)

---

## ✅ 3. Missing Value Handling
Ensures data consistency by dealing with corrupted or missing entries:

Converts non-numeric entries to NaN

Drops rows/columns with NaN values to maintain clean input

---

## ✅ 4. Column Extraction
Since each .csv file contains multiple columns, the preprocessing pipeline:

Extracts only the first column (raw ECG signal)

Converts to NumPy array for further processing

---

## ✅ 5. Visualization
Provides visual confirmation of ECG signal shape and filtering performance:

python:
record = "100"
ecg = load_preprocess_csv(record)
plt.plot(ecg[:1000])
plt.title("ECG Signal - Record 100")
plt.xlabel("Samples")
plt.ylabel("Amplitude")

---

## ✅ 6. Batch Processing
Applies the preprocessing pipeline across the full dataset:

python:
processed_data = {}

for file in os.listdir(DATA_PATH):
    if file.endswith(".csv"):
        rec_id = file.replace(".csv", "")
        ecg = load_preprocess_csv(rec_id)
        processed_data[rec_id] = ecg

---

## 🛠 Tech Stack

🐍 Language: Python

📚 Libraries: NumPy, Pandas, SciPy, Matplotlib

💻 IDE: Jupyter Notebook / VS Code

📦 Tools: Git & GitHub for version control

---
