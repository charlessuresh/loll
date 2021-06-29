# Our dashboard

We explored `explainerdashboard` API, a python library for developing interactive dashboards to illustrate the prediction results of machine learning models. Refer to the figure below as a reference to illustrate how the dashboard looks like,

- The main page of the dashboard:

![dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/dashboard.png)

- A sub-page of the dashboard to illustrate the regression part of the hurdle model: 

![sub dashboard](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-dashboard/img/sub-dashboard.png)

## Build a local dashboard

### Step 1
download `dashboard` folder to your local PC

### Step 2
activate a python env

### Step 3
run one of the following commands to install `explainerdashboard` API,

```
pip install explainerdashboard
```

or

```
conda install -c conda-forge explainerdashboard
```

### Step 4
open `dashboard.ipynb` and run the cells one by one and copy the link below with your browser,
![dashboard link](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-book/img/dashboard_link.png)

### Step 5
There is one py script (`dashboard.py`) with common functions that you can utilize to build a dashboard. 

You can import `build_dashboard` or `build_customized_dashboard` without triggering a jupyter notebook. 

