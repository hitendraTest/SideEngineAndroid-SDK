# SideEngineAndroid-SDK

Documentation

1. Minimum Requirements

        - iOS
        - xCode 12(or later)
        - Swift 5(or later)
        - CocoaPods(https://cocoapods.org/)

2. Add SideEngine SDK to your app

        - Create a Podfile if you don't already have one:
        $ cd your-project-directory
        $ pod init

3. Add the pods for the SideEngine SDK

         platform :ios, '12.1'
         pod 'SideEngineiOS', '~> 1.0.1'
        
4. Install the pods, then open your .xcworkspace file to see the project in Xcode:

        $ pod install
        $ open your-project.xcworkspace

5. Initialise SideEngine in your app

        -The final step is to add an initialisation code to your application. If you are using a quickstart sample project, this has been done for you.

         import BBSideEngine

6. Configure a SideEngine shared instance, typically in your app's application:didFinishLaunchingWithOptions: method:
 
        BBSideEngineManager.shared.configure(accessKey: "Your license key here")
        
7. Sample code here
        
        let shared = BBSideEngineManager.shared
        shared.applicationLicenseKey = "Your license key here"
        Start SideEngine
        shared.riderName = "App user name here"
        shared.startSideEngine()

* Customise the SideEngine theme(Optional).

        shared.countDownTimerLimit = Default 30 seconds
        shared.backgroundColor = Default "E93323"
        shared.contentTextColor = Default "ffffff"
        shared.swipeToCancelTextColor = Default "0B0B0B"
        shared.swipeToCancelBackgroundColor = Default "ffffff"
        shared.showLog = //Default true
        shared.impactBody = "Detected a potential fall or impact involving"
        

* Event list:

        *SideEngine events listener, sample code below:
        
        shared.sideEventsListener { (response) in
            //i.e.
            if response.type == .start && response.success == true {
                 //Update your UI here
            }
        }
        enum BBSideOperation {
            case configure //Configure side engine
            case start //Start side engine
            case stop //Stop side engine
            case sms //Returns SMS delivery status
            case email //Returns email delivery status
            case incidentDetected //Threshold reached and you will redirect to countdown page
            case incidentCancel //User cancled countdown
            case incidentAlertSent //Return the alert sent (returns alert details (i.e. time, location, recipient, success/failure)) 
            case incidentVerifiedByUser //User verified incident true or false
            case timerStarted //Countdown timer started
            case timerFinished //Countdown timer finished
        }

8. Send SMS

    - Function to send out SMS when an incident is detected(Called once per incident).
    
            let contact = ["phoneNumber": "Contact number without country
            code",
            "username": "Your emergency contact name",
            "countryCode": "Your emergency contact country
            code"]

            BBSideEngineManager.shared.sendSMS(contact: contact)
            
            
9. Send Email

 - Function to send out an Email when an incident is detected(Called once per incident).
 
        BBSideEngineManager.shared.sendEmail(toEmail: "example@gmail.com")

* SMS & Email sending requires the event below:

        shared.sideEventsListener { (response) in
            if response.type == .incidentDetected {
                //Use either one or Both
                BBSideEngineManager.shared.sendSMS(contact: contact)
                BBSideEngineManager.shared.sendEmail(toEmail: "example@gmail.com")
            }
        }


*Other configurations

- Open your project info.plist file and add location & motion permission key and description

        - Privacy - Location When In Use Usage Description
        - Privacy - Location Always and When In Use Usage Description
        - Privacy - Motion Usage Description


* Happy coding: Run your project now :)
