# Weather Forecasting for CliMate

## Table of Contents
1. [Project Overview](##project-overview)
2. [Software Requirements](##software-requirements)
3. [Hardware Requirements](##hardware-requirements)
4. [Setup and Installation Instructions](##setup-and-installation-instructions)
5. [How to Run the Project](##how-to-run-the-project)
6. [Common Issues and Troubleshooting](##common-issues-and-troubleshooting)
7. [Additional Notes](##additional-notes)
8. [Contact Information](##contact-information)

## Project Overview
This repository hosts all the machine learning components of the CliMate project. It includes Jupyter notebooks used for gathering weather data, training machine learning models for weather forecasting, and contains the exported datasets and models that will be utilized in production to make weather forecasts. 

This repository serves as the central hub for all machine learning-related activities within CliMate's project, and all further development, enhancements, and improvements can be managed and done over here.

Go through the remaining sections of this readme to set up the project and get started with contributing.

## Software Requirements

To run this project, you'll need the following software and dependencies:

- **Programming Language**: Python 3.10.8 (Only tested for python version 3.10)
- **Libraries and Frameworks**:
  - TensorFlow
  - Keras
  - Scikit-learn
  - OpenMeteo
  - Requests
  - NumPy
  - Seaborn
  - Pandas
  - Matplotlib

- **Tools**:
  - Jupyter Notebook

More detailed requirements for python dependencies are available in the requirements.txt file.

## Hardware Requirements
For development, a normal laptop is sufficient. However, it’s better if you have a laptop or workstation equipped with an NVIDIA graphics card to train the models more efficiently. If you plan to work with GPUs for machine learning model training, ensure that the correct GPU versions of CUDA and cuDNN are available. If you don't have a powerful laptop, connecting to a cloud GPU runtime can be helpful to run the model training and development on the cloud.

## Setup and Installation Instructions
Complete the following steps to complete the software setup of the project.

1. Clone this repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Make sure all software and hardware requirements are setup as mentioned earlier like *Jupyter Notebook*.
    ```sh
    pip install jupyter
    ```
    
3. Install all the Python dependencies using ```requirements.txt``` 
    ```sh
    pip install -r requirements.txt
    ```
    
4. Start a jupyter notebook server to start working with the notebooks in this project.
    ```sh
    jupyter notebook
    ```

## Usage
```sh
./wc.exe [OPTION]... [FILE]
```

## How to Run & Train Models
This repository contains the ```/dataset```, ```/models```, and ```/notebooks``` directories.

1) /notebooks
    - Contains two .ipynb notebooks - ```Fetch_Weather_Data_For_Location.ipynb``` and ```LSTM_Weather_Forecast_Model.ipynb```.
    - ```Fetch_Weather_Data_For_Location.ipynb```:
      - Fetches historical (hourly) temperature, humidity, dew point, rain, pressure, wind speed, and wind direction data for a specific location.
      - This notebook retrieves the required data to train the model, so this notebook should be run before ```LSTM_Weather_Forecast_Model.ipynb```.
      - Refer to the ```/locations``` endpoint in the ```forecast-api``` repository for an exhaustive list of location codes.
      - Refer to the in-line comments and print statments to learn more about what each cell does.
      - Before running the cells, ensure that the cells tagged with ```#TODO``` are modified accordingly.
      - ``` 
        # TODO: Change location code
        location_code = ```johor-bahru```
      - ```
        # TODO: Change to specific location's latitude and longitude
        ```latitude```: 1.4655,
        ```longitude```: 103.7578,
      - Create the corresponding file under ```/datasets```, named according to the location code (e.g. ```johor-bahru```). This is where the dataset used for machine learning training is stored.
      - Run all cells.
      - A new ```.csv``` file that contains this historical data should be expected in this newly created file. 
    - ```LSTM_Weather_Forecast_Model.ipynb```:
      - This notebook contains the implementation of the LSTM neural network used to predict weather data for one particular location.
      - This model currently predicts temperature, humidity, dew point, rain, pressure, wind speed, and wind direction based on the historical data generated from ```Fetch_Weather_Data_For_Location.ipynb```, and the LSTM model in this notebook.
      - Refer to the in-line comments and print statments to learn more about what each cell does.
      - Before running the cells, ensure that the cells tagged with ```#TODO``` are modified accordingly.
      - ``` 
        # TODO: Change location code
        location_code = ```johor-bahru```
      - Create the corresponding folder under /models, named according to the location code (e.g. ```johor-bahru```). This is where the model is stored.
      - Run all cells.
      - Note that it takes approximately 1-2 hours to train one model, depending on the device being used.
      - A new ```model.h5``` and ```scaler.pkl``` file should be expected in this newly created file. The ```model.h5``` contains the trained model; the ```scaler.pkl``` contains the Scaler object to help denormalise values of the output layer.
    - Note that all the steps above only train **ONE** model for **ONE** location. Repeat these steps for other desired locations.
2) /datasets
   - This directory contains all historical data used to train the models.
   - Subfolders, each named according to location codes, store a ```.csv``` file that represent historical data for each location.
   - These subfolders should be created before ```Fetch_Weather_Data_For_Location.ipynb``` is run.
   - Ensure these subfolders are populated with the correct ```.csv``` file before running ```LSTM_Weather_Forecast_Model.ipynb```.
3) /models
   - This directory contains all the trained LSTM models.
   - Subfolders, each named according to location codes, store a ```model.h5``` file that represent a trained model for each location.
   - These subfolders should be created before ```LSTM_Weather_Forecast_Model.ipynb``` is run.
   - The ```scaler.pkl``` will also be found here after running ```LSTM_Weather_Forecast_Model.ipynb```. This is needed to de-normalise the values in the output layer. 
   - **IMPORTANT:** Ensure that this repository (```weather-forecasting```) resides in the same directory as the ```forecast-api``` directory (i.e. they have the same parent directory). This is beacause ```/forecast``` endpoint in ```forecast-api``` searches for the models in ```/models``` using absolute paths.

## Current Machine Learning Pipeline and Model Architecture
1) Data for a particular city location in Malaysia is fetched from [OpenMeteo](https://open-meteo.com/) for the last 14 years until August 2024.
2) The data is stored in a semantic folder as a CSV file.
3) This dataset is then used in the training, but it is first preprocessed.
4) The attributes are scaled using normalization in the preprocessing stage, this is known as feature scaling.
5) The dataset is then split into a training set, a testing set, and a validation or evaluation set.
6) Then we create the LSTM model. It has the following architecture:
```python
def create_model(input_shape):
    model = Sequential()
    model.add(Bidirectional(LSTM(50, return_sequences=True), input_shape=input_shape))
    model.add(LSTM(7)) # Predicting 7 features
    model.compile(optimizer='adam', loss='mse')
    return model
```
8) The model is trained by fitting it to the training dataset.
9) The trained model after 50 epochs is evaluated using the testing dataset and the predicted and true values or plotted for visualization.

## Future Work

As we continue to improve the CliMate project, there are several potential enhancements and features to consider for future iterations:

1) Model Optimization and Hyperparameter Tuning:
   - Implement various ways to explore hyperparameter tuning using libraries like Optuna or Hyperopt to enhance model performance and accuracy.
   - Experiment with different neural network architectures and techniques, such as GRUs or Transformers, to compare performance against the current LSTM model.

2) Model experimentation with certain weather attributes
   - The current model does not capture the patterns of rain well. It can be inferred from the image below as such.
   - The rain pattern is of steps in nature. It can either be 0 or a positive real value. Due to the nature of its values, the model is not able to accurately capture its patterns.
   - Hence, it is useful to experiment with different neural network architectures and techniques and also experiment with ensemble methods by putting multiple models together.
    ![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)

3) Extended Data Sources:
   - Incorporate additional weather data sources, which could include live sources, to improve forecasting accuracy.
   - Expand the dataset to include more diverse geographical locations, allowing for broader model training and validation.

4) Automation through CI/CD pipelines
   - Development of multiple models and training and exporting them along with data preprocessing can be very labor intensive if done manually.
   - In order to tackle this, it would be useful to develop and architect a CI/CD pipeline that automates all of these.

## Common Issues and Troubleshooting

Developers might encounter the following common issues:

- **Dependency Installation Issues**: You may face problems when installing machine learning dependencies. The best sources for solving these issues are ChatGPT and StackOverflow, where you can find solutions and troubleshooting tips from the community.

- **Missing Files for Machine Learning Packages**: Sometimes, you might encounter issues where files are missing for machine learning packages. In such cases, the most effective way to resolve the problem is to reinstall the packages.

## Additional Notes
- This project has only been tested on python version 3.8
- It is inevitable that you will encounter dependencies issues and you will need to play around with the version. If there are any resulting version changes, please update them in the requirements.txt file. This is so that the whole team works with the same versioning.

## Contact Information
If you have tried all resorts but still have issues getting the project started, you may contact members of our team from the table below.

| Name                       | Email                       | Student ID |
| -------------------------- | --------------------------- | ---------- |
| Suman Datta                | sdat0004@student.monash.edu | 30668786   |
| Daryl Lim                  | dlim0036@student.monash.edu | 33560757   |
| Ryan Choo Yan Jhie         | rcho0046@student.monash.edu | 33455775   |
| Nicholas Yew               | nyew0001@student.monash.edu | 33642478   |
| Lim Zhi Cheng              | zlim0052@student.monash.edu | 33204128   |
| Mohamed Ammar Ahamed Siraj | amoh0157@student.monash.edu | 33187762   |
| Nicholas Lee               | nlee0060@student.monash.edu | 32840594   |
| Shyam Borkar               | sbor0018@student.monash.edu | 32801459   |
| Lai Carson                 | lcar0029@student.monash.edu | 32238436   |
| Hanideepu Kodi             | hkod0003@student.monash.edu | 33560625   |
