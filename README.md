# AirManagement - Use-Case Description Forecasting Energy consumption
The project aims to reduce and predict the consumption of compressed air, used in industrial production processes.
The project was divided into two areas:
1. Integration of air consumption data (instantaneous flow, pressure, temperature, total flow consumed) from the OT area to the IT area
2. Prediction of air consumption (total air flow rate consumed) of air using the architecture of Convolutional Neuronal Networks (CNN) and Generative Adversarial Network (GAN)
![image](https://github.com/ro0tst/AirManagement/assets/93845063/fd3f6e59-ff78-4d0c-994e-ab557ed6bf3b)

Integration of data from OT in IT
![image](https://github.com/ro0tst/AirManagement/assets/93845063/1e91d86f-40aa-4ca9-b30d-da1798aa5872)
To reduce air consumption, we wanted to integrate the Air Management System (AMS) industrial equipment, manufactured by SMC, into the data architecture.
Below you will find a link to the manufacturer's page
https://www.smcworld.com/webcatalog/en-jp/air-management-system/air-management-system/AMS_AB-E/#detail
The choice of this product was determined by the fact that the technical characteristics regarding data ingestion, towards the IT area, are based on the OPC UA protocol.
Data access, using the OPC UA protocol, allows us independence from the master controller of the utility, on which this device is installed. In this way, we were no longer restricted by the old data architecture, industrial processes and possible security restrictions, imposed by the manufacturer of the use we wanted to optimize.
This stage had as its final goal the capture of the data coming from the Air Management System (AMS) equipment, in real time in the Google Cloud platform (Data Wharehouse - BigQuery) and the use of BI tools (Looker Studio) for data visualization.
During the implementation of the project, there was another request, coming from an industrial partner, that the real-time ingestion of the data be done on-received, in MySQL.
![image](https://github.com/ro0tst/AirManagement/assets/93845063/a047be97-76ea-4fe8-a493-6434a5faa43c)

Forecasting
For consumption forecasting, we opted for a Depp Learning architecture of Convolutional Neuronal Networks (CNN) and Generative Adversarial Network (GAN) type
The reason why we adopted this direction was the common problem, for the adoption of ML algorithms, namely the data needed to train the models, data which in most cases are either insufficient or irrelevant for the model. Most of the time these training data require a long time in their collection which leads to a long ROI. We used the GAN architecture to generate realistic data to enrich the initial data set. Similar to power consumption, the GAN was useful to generate additional examples of airflow so that we had a more diverse and representative data set.
The choice of the CNN architecture was determined by:
Spatial representation of the data: We assumed that the data will have a time and space distribution of compressed air consumption, and CNNs can be effective in capturing these spatial relationships. Convolutional layers can help identify spatial patterns and learn features from this data.
Detecting Local Patterns: CNNs specialize in detecting local patterns in data. If there are significant local features in your data, such as sudden variations in compressed air consumption in certain regions or time intervals, CNNs can effectively identify them.
Generative dataset expansion: As our dataset was limited, Generative Adversarial Networks (GANs) could be integrated into a CNN architecture to generate additional realistic examples.
Hierarchical representation of features: CNNs are capable of learning hierarchies of features, from simple to complex. This hierarchical approach can be useful in identifying different levels of influence on compressed air consumption.

