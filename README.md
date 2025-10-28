# **🌡️ TensorFlow Temperature Forecasting Guide**

This guide details the setup and execution of an LSTM-based time series forecasting script designed to predict hourly temperatures using TensorFlow.

## **📁 Project Structure**

Your project should be organized within a root directory (e.g., Temp-Forecast/) containing the necessary files and the isolated environment.  
Temp-Forecast/  
├── 📊 sample\_temperature\_data.csv  
├── 🐍 temp\_forecast\_tf.py  
├── 📁 tf\_env/                \# Python Virtual Environment  
└── 📄 README.md

## **🔧 Setup Steps**

### **Step 1: Create Project Folder**

Use your command line interface to set up your working directory.  
\# Create project folder on Desktop  
mkdir "Temp-Forecast"  
cd "Temp-Forecast"

### **Step 2: Prepare Project Files**

Place the following two files inside your newly created Temp-Forecast/ folder:

1. **sample\_temperature\_data.csv**: The time series dataset containing hourly temperature readings.  
2. **temp\_forecast\_tf.py**: The main TensorFlow training and prediction script.

### **Step 3: Recommended Environment Setup**

Using a virtual environment is strongly recommended to isolate dependencies.  
\# Create virtual environment  
python \-m venv tf\_env  
   
\# Activate environment (Choose based on your OS)  
source tf\_env/bin/activate       \# (Linux/Mac)  
tf\_env\\Scripts\\activate         \# (Windows)  
   
\# Install dependencies  
pip install tensorflow pandas matplotlib scikit-learn

## **🧮 Sample Dataset (sample\_temperature\_data.csv)**

The model learns from historical hourly data with two key columns: Timestamp and Temperature.

| Timestamp | Temperature |
| :---- | :---- |
| 01/01/2025 00:00 | 20.49 |
| 01/01/2025 01:00 | 20.07 |
| 01/01/2025 02:00 | 21.08 |
| ... | ... |
| 10/01/2025 00:00 | 19.22 |

*The dataset covers multiple days, allowing the model to learn hourly, daily, and weekly temperature variations.*

## **💻 Step 4: TensorFlow Forecasting Script (temp\_forecast\_tf.py)**

### **Overview**

This script uses a **Long Short-Term Memory (LSTM)** neural network, which is ideal for sequence prediction tasks like time series forecasting.  
**The script handles:**

* Data cleaning, time-based interpolation, and normalization.  
* Creation of time series windows (lookback) for model training.  
* Training with **Early Stopping** and validation.  
* Evaluation using **Mean Absolute Error (MAE)** and **Mean Absolute Percentage Error (MAPE)**.  
* Visualization of results and export of a 24-hour forecast.

### **🧠 Core Workflow Breakdown**

| Component | Task |
| :---- | :---- |
| **Data Preparation** | Reads CSV, resamples hourly (1h), and fills missing data gaps via interpolation. |
| **Windowing** | Uses a sliding window (default: **72 hours**) to structure data for the LSTM. |
| **Model Training** | Builds a sequential model with two stacked **LSTM layers** and trains it. |
| **Forecast Generation** | Performs a **24-hour rolling forecast** and saves the output to a CSV file. |

### **🔢 Key Parameters to Adjust**

| Parameter | Description | Default |
| :---- | :---- | :---- |
| **FREQ** | Resample frequency of the data. | "1h" |
| **LOOKBACK** | Historical hours per window (how much past data the model sees). | **72** |
| **HORIZON** | Forecast steps ahead (how many hours into the future to predict at once). | **1** |
| **EPOCHS** | Maximum training epochs. | **20** |

## **🚀 Step 5: Run the Project**

Ensure your virtual environment is active before running the script.  
\# Activate the environment (if not already active)  
tf\_env\\Scripts\\activate   
   
\# Execute the forecasting script  
python temp\_forecast\_tf.py  
