
มีบริการมากมายที่สามารถใช้ในการ _ฝึกโมเดลแมชชีนเลิร์นนิง_ ซึ่งการเลือกใช้บริการใดนั้นขึ้นอยู่กับหลายปัจจัย เช่น

- คุณต้องการฝึก _โมเดลแบบไหน_
- คุณต้องการ _ควบคุมกระบวนการฝึก_ เองมากน้อยแค่ไหน
- คุณมี _เวลาลงทุนกับการฝึกโมเดล_ แค่ไหน
- องค์กรของคุณใช้งาน _บริการใดอยู่แล้ว_
- คุณถนัด _ภาษาโปรแกรม_ ใด

ในระบบของ Azure เองก็มีบริการหลายอย่างที่ใช้สำหรับการฝึกโมเดล _แมชชีนเลิร์นนิง_ โดยบริการที่นิยมใช้กัน ได้แก่

| Icon                                                                                                                                                                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Icon of Azure Machine Learning.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/03-01-machine-learning.png) | **Azure Machine Learning** gives you many different options to train and manage your machine learning models. You can choose to work with the Studio for a UI-based experience, or manage your machine learning workloads with the Python SDK, or CLI for a code-first experience. Learn more about [Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning).                                                                                                                                        |
| ![Icon of Azure Databricks.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/03-01-databricks.png)             | **Azure Databricks** is a data analytics platform that you can use for data engineering and data science. Azure Databricks uses distributed Spark compute to efficiently process your data. You can choose to train and manage models with Azure Databricks or by integrating Azure Databricks with other services such as Azure Machine Learning. Learn more about [Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/what-is-databricks).                                                                                                         |
| ![Icon of Microsoft Fabric.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/fabric.png)                       | **Microsoft Fabric** is an integrated analytics platform designed to streamline data workflows between data analysts, data engineers, and data scientists. With Microsoft Fabric, you can prepare data, train a model, use the trained model to generate predictions, and visualize the data in Power BI reports. Learn more about [Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/microsoft-fabric-overview), and specifically about [the data science features in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-science/). |
| ![Icon of Azure AI Services.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/03-01-cognitive-services.png)    | **Azure AI Services** is a collection of prebuilt machine learning models you can use for common machine learning tasks such as object detection in images. The models are offered as an application programming interface (API), so you can easily integrate a model with your application. Some models can be customized with your own training data, saving time and resources to train a new model from scratch. Learn more about [Azure AI Services](https://learn.microsoft.com/en-us/azure/cognitive-services/what-are-cognitive-services).                     |
## Features and capabilities of Azure Machine Learning

Let's focus on **Azure Machine Learning**. Microsoft Azure Machine Learning is a cloud service for training, deploying, and managing machine learning models. It's designed to be used by data scientists, software engineers, devops professionals, and others to manage the end-to-end lifecycle of machine learning projects.

Azure Machine Learning supports tasks including:

- Exploring data and preparing it for modeling.
- Training and evaluating machine learning models.
- Registering and managing trained models.
- Deploying trained models for use by applications and services.
- Reviewing and applying responsible AI principles and practices.

Azure Machine Learning provides the following features and capabilities to support machine learning workloads:

- Centralized storage and management of datasets for model training and evaluation.
- On-demand compute resources on which you can run machine learning jobs, such as training a model.
- Automated machine learning (AutoML), which makes it easy to run multiple training jobs with different algorithms and parameters to find the best model for your data.
- Visual tools to define orchestrated _pipelines_ for processes such as model training or inferencing.
- Integration with common machine learning frameworks such as MLflow, which make it easier to manage model training, evaluation, and deployment at scale.
- Built-in support for visualizing and evaluating metrics for responsible AI, including model explainability, fairness assessment, and others.

Next, let's see how we can get started with Azure Machine Learning in a user interface.