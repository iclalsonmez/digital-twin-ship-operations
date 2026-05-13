# Digital Twin Model for Ship Operations

This repository contains a prototype digital twin workflow for ship voyage performance analysis. The project was developed to support a Naval Architecture and Marine Engineering thesis focused on economic speed estimation, fuel consumption prediction, fuel cost calculation, and CO2 emission forecasting.

The main purpose of the project is to bring vessel particulars, voyage information, engine parameters, and environmental conditions into a single prediction workflow. The notebook is designed to run in Google Colab and includes model training, evaluation, result visualization, and an interactive voyage prediction demo.

## Project Background

Ship operation is affected by many variables, including vessel size, loading condition, engine performance, route distance, wind, waves, and sea conditions. In practice, these variables directly influence sailing speed, fuel consumption, operating cost, and emissions.

This project was prepared as an academic support tool for a thesis study in the field of Naval Architecture and Marine Engineering. It is not intended to be a commercial-grade ship performance platform. Instead, it demonstrates how machine learning models can be combined with maritime operational data to build a prototype decision-support workflow.

## What This Project Does

The workflow estimates four main outputs:

- Economic sailing speed
- Fuel consumption per voyage
- Fuel cost per voyage
- CO2 emission per voyage

The notebook uses three connected models:

1. **Economic Speed Model**  
   Predicts the most efficient operating speed of the vessel.

2. **Fuel Consumption Model**  
   Predicts total fuel consumption per voyage. The predicted economic speed is used as an additional input feature.

3. **CO2 Emission Model**  
   Predicts total CO2 emission per voyage. The model uses operational variables together with predicted fuel consumption.

A formula-based CO2 calculation is also included for comparison:

```text
CO2 = Fuel Consumption × Emission Factor
```

The emission factor used in this project is:

```text
3.114 kg CO2 / kg fuel
```

## Interactive Demo

The notebook includes an interactive voyage prediction demo built with `ipywidgets`.

The user enters operational and vessel-related information such as:

- Departure city
- Arrival city
- Sea or ocean region
- Route type
- Ship type
- Cargo weight
- Deadweight
- Main dimensions
- Engine power
- Engine load
- Specific fuel consumption
- Propeller efficiency

Environmental values such as wave height, wave period, wind speed, weather condition, and resistance-related variables are not entered manually. These values are selected automatically from the dataset according to the selected departure, arrival, and sea/ocean information.

The demo returns:

- Predicted economic speed
- Predicted fuel consumption
- Predicted fuel cost
- Predicted CO2 emission from the machine learning model
- Formula-based CO2 emission estimate


## Repository Structure

```text
digital-twin-ship-operations/
│
├── digital_twin_ship_operations.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## Dataset

The dataset is not included in this repository.

To run the notebook, place the dataset in your own Google Drive and update the dataset path inside the notebook:

```python
DATA_PATH = "/content/drive/MyDrive/Digital Twin - Ships/data.xlsx"
```

The dataset should contain voyage, vessel, engine, environmental, fuel consumption, and emission-related variables.

The main target columns used in the notebook are:

```text
Economic_Speed_knots
Fuel_Consumption_per_Voyage
Total_CO2_per_Voyage_kg
```

## Notebook Workflow

The notebook follows this order:

1. Load and clean the dataset
2. Define preprocessing, evaluation, plotting, and feature alignment functions
3. Train the economic speed model
4. Train the fuel consumption model
5. Train the CO2 emission model
6. Save model outputs, tables, and plots
7. Run the interactive voyage prediction demo

## Models Used

### Model 1: Economic Speed Estimation

The first model estimates the vessel's economic sailing speed.

Target column:

```text
Economic_Speed_knots
```

A Ridge Regression model is used as a baseline model for continuous speed prediction.

### Model 2: Fuel Consumption Estimation

The second model estimates total voyage fuel consumption.

Target column:

```text
Fuel_Consumption_per_Voyage
```

This model also uses the predicted economic speed as an additional input feature.

### Model 3: CO2 Emission Estimation

The third model estimates total CO2 emission per voyage.

Target column:

```text
Total_CO2_per_Voyage_kg
```

The model uses predicted fuel consumption together with other operational variables.

## How to Run

1. Open the notebook in Google Colab.
2. Mount Google Drive.
3. Place the dataset in the correct Drive folder.
4. Update `DATA_PATH` if needed.
5. Run the notebook cells from top to bottom.
6. Use the interactive demo at the end of the notebook.

## Requirements

Install the required packages with:

```bash
pip install -r requirements.txt
```

In Google Colab, most of the required packages are already available. If the interactive demo does not appear, run:

```python
!pip install ipywidgets -q
import ipywidgets as widgets
from IPython.display import display, clear_output
```

## Outputs

The notebook can generate:

- Trained model files
- Prediction result tables
- Test result tables
- Feature coefficient and feature importance tables
- Actual vs predicted plots
- Residual plots
- Error distribution plots

By default, outputs are saved under:

```text
/content/drive/MyDrive/Digital Twin - Ships/outputs
```

These output files are not included in the repository.

## GitHub Rendering Note

The notebook includes an interactive widget-based demo. GitHub may not always render widget outputs properly. If the notebook does not display correctly on GitHub, it should still run normally in Google Colab.

For a cleaner repository view, widget outputs can be cleared before uploading the notebook. The code remains available, and the demo can be run again in Colab.

## Limitations

This project is a prototype developed for academic support and experimentation. The results depend heavily on dataset quality, feature consistency, and how representative the operational data is.

For real-world ship performance monitoring, the model would need more detailed and reliable data, such as:

- Real AIS data
- Speed through water measurements
- Vessel heading
- Current speed and direction
- Detailed engine sensor data
- Noon reports
- More accurate wave spectrum data
- Real fuel consumption logs

## Future Work

Possible improvements include:

- Building a web-based interface
- Connecting the workflow to route-based weather APIs
- Improving the physical resistance calculation layer
- Adding anomaly detection for machinery condition monitoring
- Improving the model with real voyage and sensor data
- Deploying the workflow as a lightweight decision-support tool

## License

This project is licensed under the MIT License.
