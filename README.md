# Realtor.com: Will they or won't they? Return user prediction

- Organization name: Realtor.com
- Project mentor: Tiffany Timbers
- Partner: Tarini Bhatnagar
- Team members: Rui Wang, Yuyan Guo, Charles Suresh, Siqi Zhou

## Executive Summary
The goal of this project was to predict a user's future visits to Realtor.com website based on the user's past visit history. To achieve our prediction goal, we used domain knowledge to derive useful features and capture the users' visiting patterns and behaviors. These features were used to train and build two competent machine learning models - one that predicts the return frequency and the other that predicts the return latency. Moreover, we implemented an automated pipeline to train the models along with an interactive dashboard and a web UI (user interface) to help interpret the models and their predictions dynamically.

The deliverables for this project include:

- Two reproducible machine learning models/pipelines 
- A dashboard and a flask web UI to represent findings
- Insights on which user visiting behavior is helpful for predictions
- Recommendations on how to improve the models further

## Final Report

The final report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/project_report/_build/pdf/book.pdf).

## Usage

### Step 1: Clone this GitHub repository
Start by cloning this GitHub repository to your local machine

### Step 2: Data

The data provided to us for runnning this analysis contained the raw visit history of around 1.5 million users for the months - January 2021 to April 2021 and had a total of around 62 million records. Owing to the large size of this raw data (around 10.5 GB), it cannot be uploaded to GitHub. For maximum reproducibility of the analysis, you would need to get this data and place it at `data/UBC_MDS_2021/`

For the purposes of testing the functionality of this pipeline, we filtered out the raw visit history of 2000 users, totalling around 230,000 observations and uploaded this data to the GitHub repo instead. If you have cloned the repository to your local machine, you should already have this data located at `data/UBC_MDS_2021/`. If you intend to use this smaller dataset for running the analysis, you might get results that differ from our analysis.

If you intend to run the analysis on new data:

1. It is essential for the raw data to be in the form of parquet files and be located two levels deep from the `UBC_MDS_2021` directory (`UBC_MDS_2021/**/*`):

```
UBC_MDS_2021
├── 01_2021
│   ├── event_date=20210101
│   │   ├── 20210506_193846_00019_cest3_780c4734-d27b-4820-95df-e513fd3033fb.parquet
│   │   ├── 20210506_193846_00019_cest3_9cee8ac4-512a-456c-85c3-3e81b9d2a757.parquet
│   │   └── ...
│   ├── event_date=20210102
│   │   ├── 20210506_193846_00019_cest3_0b29e2bc-b433-4a43-878f-acd47eb45cb9.parquet
│   │   ├── 20210506_193846_00019_cest3_3d29eaa9-3981-48c9-af9e-9e27164945f2.parquet
│   │   └── ...
│   └── ...
├── 02_2021
│   ├── event_date=20210201
│   │   ├── 20210506_193846_00019_cest3_453e7dd3-9ff7-45d5-9bf8-0e16e34d3352.parquet
│   │   ├── 20210506_193846_00019_cest3_d9f6a6e0-94c6-4a10-baf1-ef1ce803ad54.parquet
│   │   └── ...
│   ├── event_date=20210202
│   │   ├── 20210506_193846_00019_cest3_03d37bbb-3752-4cd9-9216-849deb9ce0d5.parquet
│   │   ├── 20210506_193846_00019_cest3_a9db645b-0af4-463c-b92d-f15ff14ebcd2.parquet
│   │   └── ...
│   └── ...
└── ...
```

2. The raw data must have (at least) the following 33 features:

| <!-- -->    | <!-- -->    | <!-- -->    |
|-------------|-------------|-------------|
| `visitor_id`| `datetime_mst`  |`visit_id` |
|`visit_number`  |`visit_hit_number`         | `browser_name`  |
| `search_box_searches`| `social_shares`  |`property_status` |
|`email_share_success`  |`sign_in`         | `language`  |
| `listing_price`| `saved_items`  |`page_type_group` |
|`paid_vs_organic`  |`experience_type`         | `app_launch`  |
| `search_number_of_bathrooms_persist` | `move_device_type`  |`login_status` |
|`client_mapi_visitor_id_event`  |`refined_search`         | `cobroke_leads`  |
| `search_max_price_persist`|  `sign_out` |`registered_user_activity` |
| `search_number_of_bedrooms_persist`  |    `apps_type`    |`kpi_channel_view`  |
|`search_min_price_persist`| `advantage_leads`  |`basecamp` |


### Step 3: Run the Analysis Using Docker

1. Install
[Docker](https://www.docker.com/get-started)
2. At the command line/terminal
from the root directory of this project, run the following command in the bash terminal to build the docker image:

```
docker build -t realtor:1.0 .
```

3. Next, run the following commands in the bash terminal as per your requirement:

  - To run the analysis for both: Model Return Frequency and Model Return Latency:

```
# Clear out all the generated models, data files and reports
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan clean

# Generate the analysis for Model Return Frequency and Model Return Latency
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan all
```

  - To run the analysis only for Model Return Frequency:

```
# Clear out all the generated models, data files and reports for Model Return Frequency
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan clean_return_frequency

# Generate the analysis for Model Return Frequency
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan all_return_frequency
```

  - To run the analysis only for Model Return Latency:

```
# Clear out all the generated models, data files and reports for Model Return Latency
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan clean_return_latency

# Generate the analysis for Model Return Latency
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan all_return_latency
```
 
  - To run a specific part of the analysis- either for Model Return Frequency or Model Return Latency, you need to replace the 'dash' in the command below with an appropriate Makefile phony target (based on your use case):

```
docker run --rm -it -p 8888:8888 -v $(pwd):/home/jovyan realtor:1.0 make -C /home/jovyan _________
```
For a list of available Makefile phony targets and their descriptions, refer [here](doc/makefile_descriptions.md). Or you may have a look at the [Makefile itself](Makefile).


*Note: Prior to using the docker image, please make sure the docker has been configured with memory larger than the data size and sufficient CPU/GPU power(refer to Figure 4.1). For the four months data given, below is the configuration we used to set the docker desktop program. This can be set by choosing the “preference” tab under the docker program.* <br><br>
![Foo](img/docker_settings.gif)


## Models

### Model 1 - Predict number of times the user will return

- The `pickle file` of the model is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/models/model_return_frequency.pickle).

- The `feature EDA report` includes the EDA for all engineered features along with details of which features are selected for model fitting. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/feature_eda/feature_eda_model_return_frequency.pdf). The html version report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/feature_eda/feature_eda_model_return_frequency.html).

- The `training report` includes all details and documentations for the model training. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/training_report/training_report_model_return_frequency.pdf). The html version report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/training_report/training_report_model_return_frequency.html).

- The `testing report` includes all details about the predictions on test set. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/testing_report/testing_report_model_return_frequency.pdf). The html version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/testing_report/testing_report_model_return_frequency.html).

### Model 2 - Predict number of days untile the user's next return 

- The `pickle file` of the model is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/models/model_return_latency.pickle)

- The `feature EDA report` includes the EDA for all engineered features along with details of which features are selected for model fitting. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/feature_eda/feature_eda_model_return_latency.pdf). The html version report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/feature_eda/feature_eda_model_return_latency.html).

- The `training report` includes all details and documentations for the model training. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/training_report/training_report_model_return_latency.pdf). The html version report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/training_report/training_report_model_return_latency.html).

- The `testing report` includes all details about the predictions on test set. The pdf version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/testing_report/testing_report_model_return_latency.pdf). The html version of the report is available [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/doc/testing_report/testing_report_model_return_latency.html).


**Note:** For all the model reports above, we recommend reading the html version of the reports, which are rendered better comparing to pdf.


## Dashboard
We explored `explainerdashboard` API, a python library for developing interactive dashboards to illustrate the prediction results of machine learning models. Refer to the figure below as a reference to illustrate how the dashboard looks like,

- The main page of the dashboard:

![dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/dashboard.png)

- A sub-page of the dashboard to illustrate the regression part of the hurdle model: 

![sub dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/sub-dashboard.png)

Please refer the link [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-book/dashboard/dashboard.md) on how to build a dashboard. 

## Flask Web UI
We also built a **flask** web UI as a prediction demo by uploading a CSV file including engineered features and clicking the `submit` button, then returning the prediction results of two models, respectively. Refer to the figure below as a reference to illustrate how the flask web UI looks like,

![flask](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/img/flask.png)


Please refer the link [here](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-book/flask/flask.md) on how to trigger a flask web UI. 

## License
- [MIT license](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/LICENSE)

## References

- Homes for Sale, Mortgage Rates, Virtual Tours &amp; Rentals: realtor.com®. Homes for Sale, Mortgage Rates, Virtual Tours &amp; Rentals | realtor.com®. (n.d.). https://www.realtor.com/. 

- Pyspark. Getting Started - PySpark 3.1.2 documentation. (n.d.). https://spark.apache.org/docs/latest/api/python/getting_started/index.html.  

- Explainerdashboard. explainerdashboard. (n.d.). https://explainerdashboard.readthedocs.io/en/latest/. 

- Poisson regression and non-normal loss. scikit. (n.d.). https://scikit-learn.org/stable/auto_examples/linear_model/plot_poisson_regression_non_normal_loss.html. 

[Realtor.com: Will they or won't they? Return user prediction]

Copyright (C) [June 2021] [Realtor.com]
