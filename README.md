# Zamplia-Android-SDK


## Migration guide

Add it in your root build.gradle at the end of repositories:


  ```groovy
  allprojects {
		repositories {
			...
			mavenCentral()
		}
	}
  ```
  Next, add the following to the dependencies closure:

  ```groovy
    dependencies {
      implementation 'com.zamplia:zampsdk:1.0.0'
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

After syncing your project with gradle files and importing Zamplia SDK classes you can easily initialize Zamplia SDK. <br/>To initialize, use the following code snippet in onCreate method of your activity. <br/>Use Environment Enum for sandbox/production.  


  ```groovy
    ZampliaApp.getInstance().initialize(this,  Environment.PRODUCTION);
  ```
    
3. Show Offer

Create Params instance with the below code snippet. Here, you need to pass API-KEY that is provided to you by Zamplia platform. <br/>You have to use sandbox key with sandbox environment and production key with production enviornment. <br/>Here you have to set Platform and transaction Id (session id to track the user). <br/>Code snippet as below :


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

### Zamplia SDK lifeCycle methods : 

1. If Zamplia SDK is failed while initialization process then this event will receive. Ex.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMInitializationFailed() {
            ...
        }
    }
  ```

2. If Offers are not enabled in any specific cultures. Ex. <br/>Let's assume that Zamplia has not Enabled your users to take offers in USA and your user is from USA than this will receive with error message.


  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMCultureNotEnabled(String message) {
            ...
        }
    }
  ```

3. If Zamplia SDK has traced or facing any loading error than this will be invoked with error.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMInternalServerError(String message) {
            ...
        }
    }
  ```


4. You can be notified when Zamplia survey not available for the user.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMSurveyNotAvailable() {
            ...
        }
    }
  ```


5. We will notify you when user start survey with Survey data where you can get ID and reward value of survey.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMUserOpenedSurvey(SurveyData surveyData) {
            ...
        }
    }
  ```


6. You can be notified if user has closed the offer/survey window.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMWindowClosed() {
            ...
        }
    }
  ```


7. You can be notified if user has left the current survey in middle and closed the window.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMUserRejectedSurvey() {
            ...
        }
    }
  ```


8. We will notify when user gets complete the survey. We will send here SurveyData as well where ID and reward value you will receive.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMSurveyCompleted(SurveyData surveyInfo){
            Log.e("SurveyId", surveyInfo.getSurveyId());
            Log.e("RewardValue", surveyInfo.getCpi()); 
            ...
        }
    }
  ```


9. We will notify if user get terminated.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMTerminated() {
            ...
        }
    }
  ```


10. We will notify if user traced in security fails.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMSecurityFailed() {
            ...
        }
    }
  ```


11. We will notify if user has participated in the survey and has tracked in Quota requirements.

  ```groovy
    public class MainActivity extends AppCompatActivity implements ZampliaCallbacks {
        @Override
        public void onZAMQuotaFull() {
            ...
        }
    }
  ```


