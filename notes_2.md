# Goals

The main goal is know the flow in the Experiment tracking and know the tool MLFlow to register this tracking.

## Experiment tracking

Concepts:
- **ML experiment**: is a process of building an ML model.
- **Experiment run**: each trial in an ML experiment, start playin with data and hiperparameter
- **Run artifact**: any file that is associted with an ML run
- **Experiment metadata**: is the parameters in the experiment, files to train, test and valite, name of model

The experiment tracking is the process to save relevant information of the experiment, for example, *source code*, *environment*, *data*, *model*, *hyperparameter*, *metrics*, this is very usefull because is possible check the version of data or multiple experiments and *save the history of model, changes in the same*, another points is beacuse is **reproducibility**, **organization**  and **optimization**.

But where save this track:

In spreedsheets, not because:

- Error prone
- no standar formar
- not visibility and collaboration
- in the copy and paste values and result is probably the human error
- if a new DS read this, probably is very difficult to he
- the collaboration is fundamental

In MLFlow:

- is an open source platform for ML Lifecycle, it allows:
    - tracking
    - models
    - model registry
    - projects
- allows you to organize experiments and track of:
    - parameters
    - metrics
    - metadata, for example tags to search
    - artifacts
    - models
- extradata:
    - source code
    - version of code (git commit)
    - start and end time
    - author

## Getting starting with MLFlow

To run MLFlow in local is necessary create a new virtualenv with python 3, in this install mlflow: `pip install mlflow` and to run mlflow: `mlflow server --backend-store-uri {uri to database} --default-artifact-root {foldet to save artifacts}`, the **--default-artifact-root** is necesary to run, if does not used this send a exception.

## What is the mcahine learning lifecycle

This is a lifecycle in the MLOps

- data sourcing
- data labeling
- data version
- Model Management:
    - experiment tracking
        - model training
        - model evaluation
        - model architecture
    - model versioning
    - model deployment (this return to data labeling)
    - **scaling hardware (this return to experiment tracking, and send to model deployment)
- prediction monitoring

## Model Registry

Is is necessary because in every new implementing of model or in new changes in existing model to register to deploy, in case to errors or fails to do a rollback, other point is the good use of labels to send in different scenaries. The stages that offers MLFlow are: *staging*, *production* and *archive*.

> Note: is important to know that when a different version of model is change the scenary by default if exists another version this is change to *archive*, with uncheck in the pop up this one stays in the stage.

The model managment of MLFlow provides:

- model lineage
- model versioning
- stage transitions
- annotations

## MLFlow in practice

Exists differents scenaries with work with ml models:

- Single data scientist, generally competition model (kaggle or another)
- Cross functional team with one data scientist, in this exists only one model but someone in the company can check the model and how to recreate
- multiple data scientist that work in multiple ml models, in this point is necessary get a control of deploys and how to is created every model

A example of this scenaries is:

- MLFlow run in local
    - in this scenario is create a default folder with name mlruns, and in this is created the default experiment in folder 0 and only using yml meta
    - If another experiment is created this take the number 1 and save all data in artifacts
    - if run *mlflow ui* this load all experiments to show
- MLFlow using a local database and tracking server
    - generraly is used when I need test multiple hyper parameters in the model
    - is necesary run **mlflow server** and add where is saved the artifacts
    - this created one folder artifacts_local, in this is saved the artifacts of model with metadata
- MLFlow remote
    - in this scenario generally is used when multiple data scientist work in multiple model
    - using a remote server (EC2 in case of AWS), S3 to save artifacts and RDS (postgresql)
    - here is used the url of server
    - a good practice in this case is use ec2-role to access in S3, is not a good idea use a IAM user
    - another good practice is block the port and public access to RDS and use the EC2 to connect

- Some benefits in remote server are:
    - shared experiments
    - collaborate
    - give more visibilityof the data

Some limitations of MLFlow:
- does not exists Auth and Users
- data versioning
- model/data monitoring & alerting, this is outside of the scope

Some alternatives:
- Neptune
- comet
- weights & biases