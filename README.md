# Deploying ML model as Public API using FastAPI and Ngrok
This project demonstrates how machine learning models can be effectively deployed as a web service and how these services can be accessed over the internet using tools like ngrok.

## Table of Contents
- [Project Overview](#project-overview)
- [Deploy Public API](#deploy-public-api)
  - [FastAPI Server - Backend](#fastapi-server---backend)
    - [Imports and Setup](#imports-and-setup)
    - [CORS Configuration](#cors-configuration)
    - [Input Data Model](#input-data-model)
    - [Loading the Model and Scaler](#loading-the-model-and-scaler)
    - [Prediction Endpoint](#prediction-endpoint)
    - [ngrok Setup](#ngrok-setup)
    - [Run the Application](#run-the-application)
  - [Ngrok Integration](#ngrok-integration)
  - [Client-side - Request Simulation](#client-side---request-simulation)

## Project Overview
This project creates a web-based API service using FastAPI that predicts whether a person is diabetic based on certain medical input features. The prediction is made using a pre-trained machine learning model, which was previously trained and saved for this purpose. The service is made accessible to the internet via ngrok, which provides a public URL for testing and deployment purposes.

## Deploy Public API
- ### FastAPI Server - Backend
  - _FastAPI:_ The backend is built using FastAPI, which is a modern, fast web framework for building APIs with Python.
  - _Model and Scaler:_ The backend loads a pre-trained machine learning model and a scaler (used for feature normalization) from disk using the pickle library.
  - _Input Data Model:_ The data required for prediction is defined using Pydantic’s BaseModel. This includes features such as Pregnancies, Glucose, BloodPressure, etc.
  - _Prediction Endpoint:_ A POST endpoint /diabetes_prediction is created to accept input data, scale it, and then make a prediction using the loaded model. The prediction result is either "The person is not diabetic" or "The person is diabetic".
    - #### Imports and Setup
      - _FastAPI:_ A web framework to build APIs quickly with Python.
      - _Pydantic's BaseModel:_ Used to define the input data model with validation.
      - _Pickle:_ For loading the pre-trained machine learning model and the scaler.
      - _Uvicorn:_ ASGI server to run the FastAPI app.
      - _Pyngrok:_ To create a public URL for the local server using ngrok.
      - _CORSMiddleware:_ Middleware to handle Cross-Origin Resource Sharing, allowing the API to be accessed from different domains.
      - _Nest_asyncio:_ Allows running asynchronous event loops within Jupyter notebooks or environments that normally do not allow it.
    - #### CORS Configuration
      - The _origins_ variable is set to _["*"]_, meaning the API will allow requests from any origin.
      - The _CORSMiddleware_ is added to the FastAPI application to handle CORS, allowing the API to be accessible from different domains and allowing various HTTP methods and headers.
    - #### Input Data Model
      - The _diabetes_input_ class inherits from _BaseModel_ and defines the structure of the input data. It includes features like _Pregnancies, Glucose, BloodPressure_, etc., that are required for making a prediction.
    - #### Loading the Model and Scaler
      - The pre-trained diabetes prediction model and the scaler (used to standardize the input data) are loaded using the _pickle_ library. These are saved models likely trained previously on a diabetes dataset.
    - #### Prediction Endpoint
      - The _@app.post('/diabetes_prediction')_ decorator defines an endpoint that listens for POST requests at _/diabetes_prediction_.
      - The _diabetes_pred_ function takes the input data, converts it into a dictionary, extracts the relevant features, scales the input data using the loaded scaler, and then makes a prediction using the loaded model.
      - The prediction is returned as either **"The person is not diabetic"** or **"The person is diabetic"** based on the model's output.
    - #### ngrok Setup
      - The _authtoken_ is used to authenticate with ngrok.
      - A tunnel is created on port 8000, and a public URL is printed, which can be used to access the local FastAPI application from anywhere on the web.
    - #### Run the Application
      - _nest_asyncio.apply()_ is used to ensure that the async event loop can run in environments that normally wouldn't support it (like Jupyter notebooks).
      - Finally, _uvicorn.run(app, port=8000)_ starts the FastAPI application on port 8000.

- ### Ngrok Integration
  - **ngrok:** This tool is used to expose the FastAPI server running on a local machine to the internet. It provides a temporary public URL, which can be accessed from anywhere in the world.

- ### Client-side - Request Simulation
  - **HTTP Request:** A simple Python script is used to send a POST request to the FastAPI server with the input data in JSON format.
  - **Response Handling:** The server processes the input, makes a prediction, and returns the result, which is then printed on the client side.
