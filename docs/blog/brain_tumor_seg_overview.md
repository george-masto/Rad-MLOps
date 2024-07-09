# Post-Deployment Surveillance Cycle

## Brief Summary

- Contextualize MLOps principles using a concrete example: brain tumor segmentation model.
- Provide an overview of each of the main steps (e.g., Continuous Monitoring, Model Deployment) involved in updating a deployed model.
- Link to deeper dive posts for each step.

## Why Post-Deployment Surveillance?

Starting from the point where a model is already in production, it is crucial to focus on MLOps aspects to ensure its continued performance and reliability. Continuous monitoring is essential to detect errors and data drifts. When such issues are identified, and after sufficient data is collected, the model can be retrained with revised labels. Following retraining, the model must be evaluated against predefined acceptance criteria. If the model meets these criteria, it can be considered for deployment, potentially replacing the current production model.

Before fully replacing the old model, it is vital to implement preliminary checks and safeguards. Techniques like canary and shadow serving can help ensure the new model's reliability. Additionally, testing the model on previously problematic inputs—those cases that necessitated retraining—provides an extra layer of assurance.

Let's examine a summary of these steps with concrete examples using a brain tumor segmentation model.

| Step                  | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Example Tools |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Continuous Monitoring | A data drift detection algorithm runs on each brain tumor case submitted to the production pipeline. This algorithm could include: 1) checking input metadata, 2) an image-based classification model, or 3) analyzing subregional tumor volumes (e.g., enhancing tissue) using output prediction segmentation masks. Additionally, physician and end-user feedback may identify cases needing correction even if drift isn’t detected by the algorithm. It's also good practice to track production or inference distributions of various metadata/output data analyses as cases are processed in production. | - AWS ECR - AWS Lambda - Docker - Python - MLFlow |
| Ground Truth Generation | Once a “drifter” case is identified, it can be manually reviewed and labeled via a segmentation mask editor. Prediction segmentations from the current model can potentially be used as starting points. Examples of these segmentation tools include 3DSlicer, ITKSnap, RedBrick, and Encord. Ideally, this could be done in a data-versioned, user-friendly web-based segmentation tool. | - 3DSlicer - ITKSnap - RedBrick - Encord - V7 - AWS S3 |
| Model Retraining | After a certain number of cases (e.g., 50) are detected as “drifters” and their corresponding tumor segmentation ground truths have been generated, a new model can be trained via an integrated Github Actions training workflow. Consider adding new cases to both the train set and any hold-out sets to ensure the previously lacking data distribution is represented in the next step, evaluation. | - Github Actions - Python - MLFlow - Weights & Biases |
| Model Evaluation | The new model should not introduce any unwanted surprises! Use pre-selected internal and/or external test sets to evaluate the brain tumor segmentation task, ensuring metrics such as Dice, Lesion-Wise Dice, and F1 Score meet acceptance criteria. | - Github Actions - Streamlit Dashboard |
| Model Deployment | Deploy the new model using canary and shadow serving methodologies. For example, implement shadow serving where the new model's tumor segmentation predictions are produced and assessed alongside the existing model, without affecting the clinical workflow or returning results from the new model to the user. Compare the new model's predictions with the old model's predictions and any available ground truth labels. After successful preliminary checks, fully deploy the new model. | - AWS ECR - Kubernetes |

## Goals of Post-Deployment Surveillance

1. Catch cases that are not represented in your training set and iteratively improve the distributional spread of your model.
2. Ensure there is no degradation in performance on pre-selected hold-out test sets that are important for internal testing and external validation (e.g., test set or generalization set per FDA requirements).
