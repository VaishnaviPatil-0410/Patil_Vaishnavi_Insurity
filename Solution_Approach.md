##### ***TelematicsAI: Behavior-Based Insurance Pricing System***



***Problem Statement :***

***Traditional auto insurance pricing relies on static demographics (age, location, credit score) rather than actual driving behavior, resulting in unfair premiums for safe drivers and no incentive for improvement. The challenge was to build an AI system that analyzes real-time telematics data to predict driver risk and automatically integrate with policy systems for behavior-based pricing.***



***Solution Approach :***

1. ***Business Constraint and Approach: The main inspiration was to be fair to safe drivers, but how do we get that data in real life? That's what an incentive is for installing a device, which is often given in the form of a welcome discount, such as 5%. The device records real-life driver behavior like breaking patterns. If you fall under the safe category, you will receive an additional discount on the premium. Additionally, we can't penalize the risky drivers; instead, we maintain their premiums at the same level. The critical discovery was that telematics programs are discount-only - insurers can offer up to 30% off for safe drivers, but cannot charge more than standard rates. This meant optimizing for precision over recall to avoid incorrectly awarding discounts.***
2. ***Data Architecture: I chose driver-level aggregated features over trip-level granular data. Insurance policies are structured per driver, not per trip. Aggregated features (average speed, total harsh braking events) provide more stable predictions than individual trip anomalies.***
3. ***Feature Engineering: Created 18 behavioral features combining raw telematics (speed, braking) with derived safety scores. The composite scoring system (speed\_safety\_score, braking\_safety\_score) allowed the model to understand nuanced driving patterns rather than just counting violations. For example, consistent moderate speeding is different from occasional extreme speeding.***



***4. Model Selection: Evaluated 13 different algorithms systematically, including XGBoost, Neural Networks, Random  Forest, Logistic Regression, SVM, Gradient Boosting, Decision Trees, and ensemble methods. Neural Networks, SVM, and XGBoost performed all well and their test accuracy was all close, but after doing some market research, XGBoost is used by competitors like Progressive, and I think it would perform better in longer run with real-life data so I chose to go ahead with it. Also, one of the main constraints was to be transparent to customers regarding the factors affecting the premium, which is why XGBoost was the best fit for this case.***

***----------------------------------------------------------------------------------------------------------------***



***Cloud Scope :***

***Data Ingestion and Storage: The first step is to replace local CSV files with a scalable Amazon S3 data lake for central storage, using a real-time service like Amazon Kinesis for data ingestion. This approach creates a durable and infinitely scalable foundation capable of handling continuous data streams from millions of vehicles. My data\_simulator.py script is valuable here, as it defines the precise data schema that the new real-time ingestion pipeline will expect and process.***



***Data Processing and Feature Engineering: To overcome the limitations of single-machine processing, the feature engineering workflow will be migrated from pandas to a distributed engine like Apache Spark running on AWS Glue. This serverless approach allows for the efficient processing of terabytes of data by automatically scaling compute resources as needed. My feature\_engineering.py script serves as the perfect logical blueprint, as its aggregation and transformation rules will be directly translated into the new, highly scalable PySpark job.***



***Model Training and Management: Model training will be moved from a local machine to Amazon SageMaker, a dedicated ML platform. This provides access to powerful, on-demand compute resources (including GPUs), enabling me to train more complex models on massive datasets far more quickly. SageMaker also offers robust experiment tracking to systematically log and compare model performance. The core model definition and training logic within my train\_model.py can be easily adapted to run as a scalable SageMaker training job.***



***Model Deployment and Serving: To ensure the prediction service is robust and scalable, my FastAPI application will be packaged into a Docker container and deployed on a managed service like Amazon SageMaker Endpoints. This creates a highly available API that automatically scales to handle traffic fluctuations, ensuring low-latency predictions for millions of users. My api.py script is essential as it provides the complete application logic, including endpoints and data validation, which will be placed directly into the container for deployment.***



***Orchestration and MLOps: Finally, the entire process will be automated by connecting each stage into a cohesive workflow using a service like AWS Step Functions. This creates a hands-off MLOps pipeline that automatically triggers feature engineering, model retraining, and deployment as new data becomes available. The sequential order in which I currently run my scripts serves as the exact blueprint for this automated workflow, ensuring a reliable and continuously improving system without manual intervention.***



<img width="1918" height="1013" alt="q" src="https://github.com/user-attachments/assets/d0bc0645-f51e-4d44-9f61-354d138be232" />
<img width="1918" height="917" alt="e" src="https://github.com/user-attachments/assets/587cb2f0-85d5-4919-a867-88fb56440ce6" />
<img width="1918" height="926" alt="w" src="https://github.com/user-attachments/assets/0e86b2f8-d985-47ff-bc0f-1b48f4c963c1" />

***This is what the running API should look like :*** 


