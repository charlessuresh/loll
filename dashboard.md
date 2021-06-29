# Our dashboard

We used the `explainerdashboard` API, a python library for developing interactive dashboards to illustrate the prediction results of machine learning models. The figure below shows the different views of the dashboar:

- The main page of the dashboard:

![dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/dashboard.png)

- A sub-page of the dashboard to illustrate the regression part of the hurdle model: 

![sub dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/sub-dashboard.png)

## Build a local dashboard

Before you build and run the dashboard, ensure that

1. `model_return_frequency.pickle`, `regression_model_return_latency.pickle` and `classification_model_return_latency.pickle` model files are already in the `models/` directory
2. The engineered features along with the targets for the test data are in parquet file format in `data/model_return_frequency/testing_data` (for the Return Frequency Model) and in `data/model_return_latency/testing_data` (for the Return Latency Model)

You can make use of the GNU Make command: `make all` to generate the files mentioned above.

There are two ways to build the dashboard. You may either use the docker container (Option 1) or you may create a conda environment and build the dashboard locally

### Option 1: Using Docker

#### Step 1
Start by cloning this GitHub repository to your local machine

#### Step 2
Install
[Docker](https://www.docker.com/get-started)

#### Step 3

At the command line/terminal
from the root directory of this project, run the following command in the bash terminal to build the docker image:

```
docker build -t realtor:1.0 .
```
#### Step 4

Next, run the following command in the bash terminal to build the dashboard:

```
docker run --rm -it -p 5000:5000 -v $(pwd):/home/jovyan realtor:1.0 python dashboard/dashboard.py --model_dir=models/ --test_data_return_frequency_dir=data/model_return_frequency/testing_data --test_data_return_latency_dir=data/model_return_latency/testing_data

```

#### Step 5

Once the dashboard is built, go to `0.0.0.0:5000` in your browser to access the dashboard


### Option 2: Run Locally

#### Step 1
Start by cloning this GitHub repository to your local machine

#### Step 2
From the root of the repository, run the following command to create and activate conda environment using the provided `yml` file:
```
conda env create -f env-return-user.yml
conda activate return_prediction
```

#### Step 3
Run the following command in the bash terminal to build the dashboard:
```
python dashboard/dashboard.py --model_dir=models/ --test_data_return_frequency_dir=data/model_return_frequency/testing_data --test_data_return_latency_dir=data/model_return_latency/testing_data

```

#### Step 4

Once the dashboard is built, copy the IP address and the port number mentioned in the terminal and paste it in your browser to access the dashboard

