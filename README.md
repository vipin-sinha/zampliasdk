# Zamplia-Android-SDK


## Migration guide

Add it in your root build.gradle at the end of repositories:


  ```groovy
  allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
  ```
  Next, add the following to the dependencies closure:

  ```groovy
    dependencies {
      implementation("com.github.vipin-sinha:zampliasdk:1.0.0")
      ...
     }
  ```

  And synchronize the project with the gradle files.

### Quick Guide

    1. Obtain a Publisher Account.
    2. Download and implement ZampliaSDK.
    3. Sync app module with your gradle files.
    4. Embed Zamplia in your code and initialize SDK.
    5. Implement ZampliaCallbacks to listen events.
    6. Use Environment.PRODUCTION before publishing your app to Google Play Store.
    7. Request your sales manager for your account to get verify.

#### Implement Zamplia in your code

1. Import Zamplia Classes


  ```groovy
  import com.zamplia.zampliasdk.ZampliaApp;
  import com.zamplia.zampliasdk.builder.Params;
  import com.zamplia.zampliasdk.callback.Environment;
  import com.zamplia.zampliasdk.callback.SurveyData;
  import com.zamplia.zampliasdk.callback.ZampliaCallbacks;
  ```


    2. Initialize Zamplia SDK

        After syncing your project with gradle files and importing Zamplia SDK classes you can easily initialize Zamplia SDK. To initialize, use the following code snippet in onCreate method of your activity. Use Environment Enum for sandbox/production.  

        ```groovy
            ZampliaApp.getInstance().initialize(this,  Environment.PRODUCTION);
        ```
    
    3. Show Offer

        Create Params instance with the below code snippet. Here, you need to pass API-KEY that is provided to you by Zamplia platform. You have to use sandbox key with sandbox environment and production key with production enviornment. Here you have to set Platform and transaction Id (session id to track the user). Code snippet as below :

        ```groovy
            Params mParams = new Params.Builder("API-KEY").setPlatform("Android").
                            setTransactionId("SESSON-ID").build();
        ```

        After creating instance of Params to get the offer use the below code snippet : 

        ```groovy
            ZampliaApp.showAvailableSurveys(this, mParams, this);
        ```

    4. Get Events from Zamplia SDK

        We have the following listeners. To use this you have to implement ZampliaCallbacks interface in your activity.

        ```groovy
            AppCompatActivity implements ZampliaCallbacks
        ```

        The following are the methods this will override :


