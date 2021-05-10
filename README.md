# DevopsApp
Example app for android continuous delivery for the course [DD2482](https://www.kth.se/student/kurser/kurs/DD2482?l=en) Automated Software Testing and DevOps.

## Prerequisite
We assume that you have already your app deployed on Google Play Store. And you'll also need the key used to sign the deployed APK. If not we invite you to follow the [Google tutorial](https://support.google.com/googleplay/android-developer/answer/9859152?hl=en).

## Setup the access to Google Play Console
- Go on [Google Play Console](https://play.google.com/console), here you can see your apps.

- Go on *Settings*, *Developer account*, *API access*. Here you can either link to an existing project or create a new one

- Click on *create a new service account* and follow the link.

- On the Google Cloud Platform, click on *CREATE SERVICE ACCOUNT* and give a name and description. And add basic editor access.

- Go back on the console, you can see the service account.

- Grant the access to the service account with the default permission.

- On the google cloud platform, generate a new JSON key and save it


## GitHub

### Action
As you can see here, we have our script for our GitHub action triggered on master branch. The fist step will generate and sign the release APK using the key we set up in the GitHub secrets and store it in the action artifacts.

The second step will get the signed APK from the action artifact and upload it to the Google Play Store using the service account created before. Here we also set up the same package name as our project and on which track we want to deploy. For more info about this settings, check the [Google tutorial](https://support.google.com/googleplay/android-developer/answer/9859152?hl=en).

### Secrets

To add your GitHub secrets, go on *Settings* and *Secrets*. The secrets works as a key-value store. Here you'll need the same key used to sign your app already deployed. 

And you need to add these secrets:

- **ALIAS**: Alias of your key
- **KEY_PASSWORD**: Password of your key
- **KEY_STORE_PASSWORD**: Password of your key store
- **SIGNING_KEY**: Your actual key in Base64 format.
  - To convert it run this command in your terminal : `openssl base64 < path_to_the_key | tr -d '\n' | tee some_signing_key.jks.base64.txt` This will create a txt file with your key in Base64 format. 
- **SERVICE_ACCOUNT_JSON**: The content of the json file downloaded when you generated the key for the service account.
