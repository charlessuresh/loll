# Our flask web UI

We built a **flask** web UI that allows users to input values for engineered features and get the prediction results of the two models- Return Frequency and Return Latency, respectively, on clicking the `Submit` button. The figure below shows what the flask web UI looks like:

![flask](https://github.com/UBC-MDS/realtor_will_they_return/blob/main/img/flask.png)


## Trigger a local flask app

### Step 1
Start by cloning this GitHub repository to your local machine

### Step 2
From the root of the repository, run the following command to create and activate conda environment using the provided `yml` file:

```
conda env create -f env-return-user.yml
conda activate return_prediction
```

### Step 3
Change the working directory to `flask/` by using the following command:
```
cd flask
```

### Step 4
Run the commond: `python app.py` or `flask run` and copy the link below and paste it in your browser
<br><br>
![flask](https://github.com/UBC-MDS/realtor_will_they_return/blob/FTR-SIQI-book/img/runpy.png)
