# TelematicsAI - Insurance Risk Assessment & Policy Integration

An AI-powered telematics solution that analyzes driver behavior and automatically integrates with insurance policy systems for real-time premium adjustments.

## Overview

TelematicsAI transforms traditional demographic-based insurance pricing into a fair, behavior-based system. The solution uses XGBoost machine learning to assess driver risk from actual driving patterns (speed, braking, acceleration), achieving 83.2% accuracy while maintaining real-time performance (<200ms API response).

Key Innovation: Implements discount-only pricing model aligned with telematics business requirements - rewarding safe drivers with up to 30% savings while maintaining standard rates for others.


## Architecture

```
Data Generation → Feature Engineering → ML Training → API Deployment → Dashboard Interface
       ↓                  ↓                 ↓              ↓               ↓
Synthetic Data     18 Features      XGBoost Model    FastAPI Server   Streamlit UI
```

<details>
<summary><strong>Prerequisites</strong></summary>

### System Requirements
- Python 3.8 or higher
- pip package manager
- 4GB RAM minimum
- Port 8000 and 8501 available

</details>

<details>
<summary><strong>Quick Start</strong></summary>

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/telematics-ai.git
cd Patil_Vaishnavi_Insurity
```
### 2. Install Dependencies
```bash
   Linux or macOS:
   python3 -m venv venv
   source venv/bin/activate

   Windows (Command Prompt):
   python -m venv venv
   venv\Scripts\activate

   Windows (PowerShell):
   python -m venv venv
   venv\Scripts\Activate.ps1
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Running the Project
```bash
1. Run the data simulator:
   python src/data_simulator.py

2. Run feature engineering:
   python src/feature_engineering.py

3. Train the model:
   python src/train_model.py

4. (Optional) Run quick accuracy check:
   python src/quick_accuracy_check.py

5. (Optional) Run model comparison:
   python src/model_comparison.py

6. Start the FastAPI service. Open a new terminal, navigate to the project folder, activate the virtual environment, and run:
   python -m uvicorn src.api:app --reload --host 0.0.0.0 --port 8000

7. Start the Streamlit dashboard:
   streamlit run src/dashboard.py

```

</details>

<details>
<summary><strong>📁 Project Structure</strong></summary>

```
telematics-ai/
├── .env                          # Environment variables
├── .gitignore                    # Git ignore file
├── requirements.txt              # Python dependencies
├── README.md                     # This file
├── Solution_Approach.md          # Soltuion of the problem explained
├── src/
│   ├── src
│   ├── api.py
│   ├── dashboard.py
│   ├── data_simulator.py
│   ├── feature_engineering.py
│   ├── train_model.py
│   ├── quick_accuracy_check.py (optional)
│   └── model_comparison.py (optional)
├── models/
│   ├── discount_eligibility_model.pkl  # Trained XGBoost model....etc
├── data/
│   ├── telematics_data.csv    # Raw simulated data
│   ├── ml_ready_dataset.csv   # Processed features
│   ├── business_analysis.csv  # Business metrics
│   └── model_comparison_results.csv  
└── docs/
    └── ModelDevelopment.ipynb
└── bin/
    └── run.sh

```

</details>

<details>
<summary><strong>🔧 Testing</strong></summary>

```bash
You can validate the model and API by:
- Checking accuracy results with the optional scripts
- Querying the API endpoints on http://localhost:8000
- Using the Streamlit dashboard for visual analysis
```

<details>
<summary><strong>API Usage : </strong></summary>

```bash
X-API-KEY: telematics_ai_secret_key_2024
```
</details>


<details>
<summary><strong>💻 Project Features</strong></summary>
The system includes:
- A data simulator to generate telematics data
- Feature engineering pipeline for driver-centric data
- Model training scripts
- Accuracy checks and model comparison utilities
- FastAPI service for serving predictions
- Streamlit dashboard for visualization


</details>

## Cloud scalability scope : 
Data Ingestion and Storage: The first step is to replace local CSV files with a scalable Amazon S3 data lake for central storage, using a real-time service like Amazon Kinesis for data ingestion. This approach creates a durable and infinitely scalable foundation capable of handling continuous data streams from millions of vehicles. My data_simulator.py script is valuable here, as it defines the precise data schema that the new real-time ingestion pipeline will expect and process.

Data Processing and Feature Engineering: To overcome the limitations of single-machine processing, the feature engineering workflow will be migrated from pandas to a distributed engine like Apache Spark running on AWS Glue. This serverless approach allows for the efficient processing of terabytes of data by automatically scaling compute resources as needed. My feature_engineering.py script serves as the perfect logical blueprint, as its aggregation and transformation rules will be directly translated into the new, highly scalable PySpark job.

Model Training and Management: Model training will be moved from a local machine to Amazon SageMaker, a dedicated ML platform. This provides access to powerful, on-demand compute resources (including GPUs), enabling me to train more complex models on massive datasets far more quickly. SageMaker also offers robust experiment tracking to systematically log and compare model performance. The core model definition and training logic within my train_model.py can be easily adapted to run as a scalable SageMaker training job.

Model Deployment and Serving: To ensure the prediction service is robust and scalable, my FastAPI application will be packaged into a Docker container and deployed on a managed service like Amazon SageMaker Endpoints. This creates a highly available API that automatically scales to handle traffic fluctuations, ensuring low-latency predictions for millions of users. My api.py script is essential as it provides the complete application logic, including endpoints and data validation, which will be placed directly into the container for deployment.

Orchestration and MLOps: Finally, the entire process will be automated by connecting each stage into a cohesive workflow using a service like AWS Step Functions. This creates a hands-off MLOps pipeline that automatically triggers feature engineering, model retraining, and deployment as new data becomes available. The sequential order in which I currently run my scripts serves as the exact blueprint for this automated workflow, ensuring a reliable and continuously improving system without manual intervention.


## License

This project is intended for academic and demonstration purposes. Please review the repository for license details.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## Contact


For questions or support, please contact [vaishnavirpatil0410@gmail.com]
