# Postmarket Surveillance of ML Model Pipelines in Medical Imaging: An MLOps Perspective

## Audience

This post is intended for healthcare professionals, medical imaging specialists, data scientists, and AI/ML engineers who are involved in the development, deployment, and maintenance of machine learning (ML) models in medical imaging.

## What is Post-Deployment Surveillance?

Post-deployment surveillance is the continuous monitoring and evaluation of ML models once they are deployed in a clinical setting. This process ensures that the models perform as expected and continue to provide accurate and reliable results for medical image analysis.

## Why is it Necessary?

### Model Drift

Model drift is a critical challenge in maintaining the performance of ML models over time. It can manifest in two main forms: data drift and concept drift.

#### Data Drift

Data drift refers to the change in the distribution of serving data compared to the training data.

##### Example:

- Adjustments in scan parameters due to hardware upgrades or time constraints can significantly alter the input data.

##### Detecting drift:

- **Subgroup Assessment**: Identify specific subgroups (e.g., gender, age, image slice thickness) to monitor differences in distribution.
  - Examine outliers and perform a comparative analysis against the larger dataset.
  - Utilize statistical methods like k-means clustering to understand performance across parameters.
- **Metric and Threshold Definition**: Establish metrics and thresholds to quantify and detect drift.
  - For instance, a shift in the demographic distribution from the training to serving data should trigger an alert.
- **Action Plan Development**: Create protocols for responding to detected drift.
  - Engage with end-users to determine the impact on model performance.
  - Acquire new data to address gaps, such as underrepresented groups.
- **Anticipation of Drift Scenarios**: Predict common scenarios where drift may occur.
  - Stay informed about changes in imaging protocols or the adoption of new medication guidelines that could affect data.

#### Concept Drift

Concept drift occurs when the definition or interpretation of labels in serving data evolves.

##### Example:

- The clinical definition of certain pathologies, such as edema in brain tumor MRIs, may be revised to reflect new medical insights or standards.

##### Overcoming concept drift:

- **Post-Inference Adaptation**: Modify software to recognize and classify new definitions in the post-inference phase.
- **Model Retraining**: Periodically update models to align with the current clinical definitions and practices.
- **Continuous Monitoring**: Implement regular reviews to quickly identify and respond to concept drift.

### From an MLOps Perspective

Ensuring the robustness of ML models in the medical imaging space through post-deployment surveillance is an essential component of MLOps. The following MLOps strategies are vital:

- **Automated Monitoring**: Use automated systems to monitor model performance and data quality in real-time.
- **Versioning Data and Models**: Keep meticulous records of data and model versions to track changes and facilitate rollbacks if necessary.
- **Continuous Training Pipelines**: Develop pipelines that can continuously train models with new data as it becomes available.
- **Collaboration with Clinicians**: Maintain a close collaboration with medical professionals to understand clinical changes that might affect model performance.

By integrating these MLOps practices, healthcare organizations can ensure that their ML models remain accurate, reliable, and effective in improving patient outcomes through advanced medical imaging analysis.
