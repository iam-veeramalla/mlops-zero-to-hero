Please refer to the below documentation for this lecture.

https://mlflow.org/docs/2.4.2/quickstart.html#install-mlflow


$ mkdir mlflow-basic-install

$ cd mlflow-basic-install

$ python3 -m venv .venv

$ source .venv/bin/activate

$ python3 -m pip install mlflow


 What it does:
Installs:
 1.MLflow Tracking
 2.MLflow UI
 3.MLflow Model Registry


Verify installation
$ mlflow --version

-> Start MLflow UI
$ mlflow ui --backend-store-uri sqlite:///mlflow.db --port 7006


What this command does :

1. mlflow ui ->	Starts the MLflow web interface
2. --backend-store-uri ->	Location to store experiment metadata
3. sqlite:///mlflow.db -> Uses SQLite DB file in current directory
4. --port 7006 -> Runs UI on port 7006

This will create: 
  -> mlflow.db
which stores:
     ->   Experiments
	 ->	  Runs
     ->   Parameters
	 ->	  Metrics
     ->   Tags

Access MLflow UI in browser:


http://localhost:7006
