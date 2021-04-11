---
layout:     post
title:      GCP Service Project Application with Flask Web Service
subtitle:   Google app engine, google datastore, google cloud storage(bucket)
date:       2021-04-04
author:     Shuo Wang
header-img: img/art-Anaconda-TensorFlow.jpg
catalog: true
tags:
    - google datastore (NoSQl)
    - Flask
    - google cloud storage
    - google app engine
    - 
---


# Configure the development environment for the experiment
1. Download SDK and App Engine, which can be downloaded online  
`gcloud components update`   
to update google cloud SDK  
2. initialization gcloud make a configuration  
`gcloud init`  
In this part, it will show login account in this computer, e.g.  
`Choose the account you would like to use to perform operations for this configuration:  
[1] XXX@gmail.com  
[2] Log in with a new account`
then you can select which account you would like to select.  
3. Create a project
`gcloud projects create [YOUR_PROJECT_ID] --set-as-default`
`gcloud app create --project=[YOUR_PROJECT_ID]`

4. Create a new virtual environment for code runing
`python -m venv env
source env/bin/activate`

5. Deploy app to Google App Engine
`gcloud app deploy
gcloud app browse`

**Attension:**
1. remember to **enable billing** to your project in order for the application to be deployed to App Enginee  
2. login google account in the console by 
`gcloud auth application-default login`
3. control python version to 3.8.* in current date

# Connect google cloud datastore 


# Connect google cloud storage
