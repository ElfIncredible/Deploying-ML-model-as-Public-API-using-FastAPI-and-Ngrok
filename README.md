# Deploying ML model as Public API using FastAPI and Ngrok
This project demonstrates how machine learning models can be effectively deployed as a web service and how these services can be accessed over the internet using tools like ngrok.

## Table of Contents
- [Project Overview](#project-overview)
- [Deploy Public API](#deploy-public-api)

## Project Overview
This project creates a web-based API service using FastAPI that predicts whether a person is diabetic based on certain medical input features. The prediction is made using a pre-trained machine learning model, which was previously trained and saved for this purpose. The service is made accessible to the internet via ngrok, which provides a public URL for testing and deployment purposes.

## Deploy Public API
- ### FastAPI Server - Backend
  - FastAPI: The backend is built using FastAPI, which is a modern, fast web framework for building APIs with Python.
  - Model and Scaler: The backend loads a pre-trained machine learning model and a scaler (used for feature normalization) from disk using the pickle library.
  - Input Data Model: The data required for prediction is defined using Pydantic’s BaseModel. This includes features such as Pregnancies, Glucose, BloodPressure, etc.
  - Prediction Endpoint: A POST endpoint /diabetes_prediction is created to accept input data, scale it, and then make a prediction using the loaded model. The prediction result is either "The person is not diabetic" or "The person is diabetic".

- ### Ngrok Integration
  - ngrok: This tool is used to expose the FastAPI server running on a local machine to the internet. It provides a temporary public URL, which can be accessed from anywhere in the world.

- ### Client-side - Request Simulation
  - HTTP Request: A simple Python script is used to send a POST request to the FastAPI server with the input data in JSON format.
  - Response Handling: The server processes the input, makes a prediction, and returns the result, which is then printed on the client side.
