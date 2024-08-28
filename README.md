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

1) Clone the repo (add code snippets if have time)
2) Make sure all the other software and hardware requirements are available on the system as mentioned earlier.
3) Install the requirements in requirements.txt using pip


## How to Run & Train Models
Discusses the structure of this repository like what is the use for datasets, models and notebooks directories. (add code snippets if have time)

1) Discuss Notebooks directory
    - Talk about the notebooks inside what are their intentions
    - how developers can create new notebooks to develop new implemtations of weather forecasting
    - Explain how there are many locations and the notebooks are for particular locations
    - Explain how the team is currently using LSTM neural architecture to create the prediction model
    - Discuss about running fetch data notebook to export location hourly weather 
    - then run the LSTM model notebook with changed location code to get the exported weather dataset to train new model for a particular location
    - give instructions on changing the location code based on the backend to create dataset and start development
2) Discuss datasets directory
3) Discuss the models directory and how it will be used for integration with the FASTAPI backend.


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
