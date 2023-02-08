<h1><b>Sensor Fault Detection</b></h1>
<br>
<h3>Problem Statement</h3>
<br>
<p>There is a Company(XYZ).There are Vehicles running across the world. Every vehicles contains some sensors their Mechanical Engineer team they have designed a Air Pressure System, Which contains some sensor.It is used for the Braking System to Improve the braking system. If some of the vehicle is not in good condition we have to identidy whether the problem is due to Air-Pressure system or not. If there is any failure in the vehicle that is because of Air-Pressure system or not. Predict Whether the Problem is from Air-Pressure system or not.</p>
<br>
<a href="https://archive.ics.uci.edu/ml/datasets/APS+Failure+at+Scania+Trucks#">DataSet Link</a>
<br>
<p>
The dataset consists of data collected from heavy Scania
trucks in everyday usage. The system in focus is the
Air Pressure system (APS) which generates pressurised
air that are utilized in various functions in a truck,
such as braking and gear changes. The datasets'
positive class consists of component failures
for a specific component of the APS system.
The negative class consists of trucks with failures
for components not related to the APS. The data consists
of a subset of all available data, selected by experts.

-- Challenge metric

Cost-metric of miss-classification:

Predicted class | True class |
| pos | neg |
-----------------------------------------
pos | - | Cost_1 |
-----------------------------------------
neg | Cost_2 | - |
-----------------------------------------
Cost_1 = 10 and cost_2 = 500

The total cost of a prediction model the sum of 'Cost_1'
multiplied by the number of Instances with type 1 failure
and 'Cost_2' with the number of instances with type 2 failure,
resulting in a 'Total_cost'.

In this case Cost_1 refers to the cost that an unnessecary
check needs to be done by an mechanic at an workshop, while
Cost_2 refer to the cost of missing a faulty truck,
which may cause a breakdown.

Total_cost = Cost_1*No_Instances + Cost_2*No_Instances.
</p>
<br>
<hr>
<br>
<h2>Training Pipeline</h1>
<br>
<p>If you have Vehicle around the world how we are going to get the reading of sensors from thier vehicles.IOT devices,Sensors are Straming data(real time data), everyday we have to get the reading from the vehicle this task will be handled by data Engineer [Big Data] team where they will dump their records in some storage space.</p>
<p>
Data Engineer[Building the Pipeline]<ul>
    <li>Getting the data from various Devices and dumping in some data bases.</li>
    <li>Kafka Cluster(It is used for the straming data only)</li></ul>
</p>
<img src="/config/workspace/Images/Kafka_cluster.jpg">
<ul><h3>Kafka Cluster</h3>
<li>Horizontally Scalable</li>
<li>It can receive the data in real time and provide data in real time(mongodb).</li>
<li>It stores the data for specified time and deleted the request</li>
<li>It can handle huge request</li></ul>
<hr>
<br>
<img src="/config/workspace/Images/training_pipeline.jpg">
<h1>Training Pipeline</h1>
<p>The Pipeline is Composed by components arranged in specific order.</p><br>
<h1>Data Ingestion</h1>
<p>Bring the data from the mongodb and create three files Training ,testing ,Validation in artifact folder</p><br>
<h1>Data Validation</h1>
<p>We have to validate the file/data like datatypes,no of columns,null values,numeric,categorical,check whether any datadrift occured</p><br>
<h1>Data Transformation</h1>
<p>Exploratory Data Analysis,Feature Engineering,Feature Scaling,Standardization,Encoding Techniques,Feature Selection,Principal Component Analysis</p><br>
<h1>Model Trainer</h1>
<p>Train the Data with different machine learning model and find the best model,fine tune the model with hyperparameter tuning the model we found the xgboost perform best with our sensor data so we used that model in the pipeline</p><br>
<h1>Model Evaluation</h1>
<p>Always Model is used in production now, we are creating new model we cannot change the production model.we have to compare it both based on that we can replace when it is better even with the testing model also.</p><br>
<h1>Model Pusher</h1>
<p>Model pusher is going to push your model into production if your trained model is better than production model deploy in the production</p><br>
<h1>Entity</h1>
<p>An Entity is a light weight persistence domain object.An entity represents a tables in a relational database and each enitity instance corresponds to a row in that table.</p>
<p>The Primary Programming artifact of an entity is the entity class,although entities can use helper classes. We are going to categorize Input/Output as entity for the databse purpose.</p>
<h2>Artifact</h2>
<ul>
<li>An artifact is an machine learning term that describes the output[a fully trained model, a model checkpoint] created by the training pipeline.</li></ul>
<p>Each o/p file that we will generate we will try to store it in single folder.folder artifact-->to store all the o/p files we have to create a artifact folder whenever we run the training pipeline it should also include the timestamp.</p>