---
title: Cloud Foundry
description: Learn how to integrate Casdoor with Cloud Foundry to secure your applications.
keywords: [OAuth, Cloud Foundry, integration]
authors: [RanTao123]
---

Before the integration, we need to deploy Casdoor locally.

Then, we can quickly implement a Casdoor-based login page in our own app with the following steps.

## Step 1: Configure Casdoor application

1. Create or use an existing Casdoor application.
2. Add a redirect URL: `http://CASDOOR_HOSTNAME/login`
   ![Casdoor Application Setting](/img/integration/java/CloudFoundry/cas.png)
3. Copy the client ID; we will need it in the following steps.

## Step 2: Add a user in Casdoor

Now that you have the application, but not a user, you need to create a user and assign the role.

Go to the "Users" page and click on "Add user" in the top-right corner. This opens a new page where you can add the new user.

Save the user after adding a username and the organization "Cloud Foundry" (other details are optional).

Now, you need to set up a password for your user, which you can do by clicking on "Manage your password".

Choose a password for your user and confirm it.

## Step 3: Build the Cloud Foundry App

Start the Cloud Foundry by following these steps.

* $ git clone git://github.com/cloudfoundry/uaa.git
* $ cd uaa
* $ ./gradlew run
  ![Casdoor Application Setting](/img/integration/java/CloudFoundry/command.png)

## Step 4: Integrate Casdoor

Now open another command line and input:

```bash
curl '<http://localhost/oauth/authorize?response_type=token&client_id=app&scope=openid&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2Fapp%2F>' -i -X GET \
  -H 'Accept: application/x-www-form-urlencoded'
```

We have already obtained the client ID and redirect URI before; we input these parameters.
![Casdoor Application Setting](/img/integration/java/CloudFoundry/parameter.png)

Execute the command, and we can get the result below, which means that we have successfully integrated Casdoor with Cloud Foundry.
![Casdoor Application Setting](/img/integration/java/CloudFoundry/result.png)

![Casdoor Application Setting](/img/integration/java/CloudFoundry/login.gif)
