# ai-genkit-rag
Build gen AI features powered by your data with Genkit

## Set up your development environment
Verify your Node.js version - v23.6.0
In your terminal, verify that you have Node.js version 20.0.0 or higher installed:

``` terminal
node -v
```

If you don't have Node.js version 20.0.0 or higher, download the latest LTS version and install it.
https://nodejs.org/


## Install the Firebase CLI
1. Verify that you have the Firebase CLI installed and that it's version 13.6 or higher:
``` terminal
firebase --version
```
2. If you have the Firebase CLI installed, but it's not version 13.6 or higher, update it:
``` terminal
npm update -g firebase-tools
```
3. If you don't have the Firebase CLI installed, install it: 
``` terminal
npm install -g firebase-tools
```

## Log into Firebase
In your terminal, log in to Firebase:
``` terminal
firebase login
```

##  Install Google Cloud's gcloud CLI
Install the gcloud CLI. https://cloud.google.com/sdk/docs/install
 ```
 (New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")

& $env:Temp\GoogleCloudSDKInstaller.exe
    
```
In your terminal, log into Google Cloud:
``` terminal
gcloud auth login
```

##  Enable Vertex AI
Use the gcloud CLI to set up Vertex AI. For all the commands on this page, make sure to replace YOUR_PROJECT_ID with the ID of your Firebase project.

In your terminal, set the default project for the Google Cloud SDK:
``` terminal
gcloud config set project YOUR_PROJECT_ID
```

If you see a warning message saying "WARNING: Your active project does not match the quota project in your local Application Default Credentials file. This might result in unexpected quota issues.", then run the following command to set the quota project:
``` terminal
gcloud auth application-default login
gcloud auth application-default set-quota-project YOUR_PROJECT_ID
```

Enable the Vertex AI service in your project:
``` terminal
gcloud services enable aiplatform.googleapis.com
```

## Configure the Firebase CLI to target your project

To make the Firebase CLI execute all commands against your Firebase project, run the following command:
``` terminal
firebase use YOUR_PROJECT_ID
```

##  Import sample data into Firestore
So that you can get started quickly, this codelab provides you with pre-generated sample data for Firestore.

To allow the local codebase to run code that would normally use a service account, run the following command in your terminal:
``` terminal
gcloud auth application-default login
```

This will open a new tab in your browser. Log in using the same Google Account you used in the previous steps.
To import the sample Firestore data, run the following commands:
``` terminal
cd load-firestore-data
npm ci
node index.js YOUR_PROJECT_ID
cd ..
```