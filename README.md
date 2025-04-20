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


##  Connect your web app to your Firebase project
Your web app's codebase needs to be associated with the correct Firebase project to utilize its services, such as the database. To accomplish this, you need to add your Firebase configuration to your app's codebase. This configuration includes essential values like your project ID, your app's API key and app ID, as well as other values that enable your app to interact with Firebase.

1. Obtain your app's Firebase configuration:
a. In the Firebase console, navigate to your Firebase project.
b. In the left-side panel, click the gear icon next to Project Overview and select Project settings.
c. In the "Your apps" card, select your web app.
d. Under the "SDK setup and configuration" section, select the Config option.
e. Copy the snippet. It begins with const firebaseConfig ....
2. Add your Firebase configuration to your web app's codebase:
In your code editor, open the src/lib/genkit/genkit.config.ts file.
Replace the relevant section with the code that you copied.
Save the file.


## Preview the web app in your browser
In your terminal, install dependencies and then run the web app:
``` terminal
npm install
npm run dev:next
```

In your browser, navigate to the locally hosted Hosting URL to view the web app. For example, in most cases, the URL is http://localhost:3000/ or something similar.