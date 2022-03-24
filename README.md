# X_CUBE_AWS_2.2.1_QC_Patch
Prepare X_CUBE_AWS2.2.1 For Quick connect

- Clone the repo in your **STM32CubeExpansion_Cloud_AWS_V2.2.1** directory

![X_CUBE_AWS_2 2 1_QC_Patch](https://user-images.githubusercontent.com/41168224/160009472-25c10564-b7f2-4365-a5bb-6e4496d480b2.png)

- Navigate to **X_CUBE_AWS_2.2.1_QC_Patch**
- run Python **apply_patch.py**
- Open STM32CubeIDE new work space
- Import the projects present in the **\Projects\B-L4S5I-IOT01A\Applications** directory

- Open **aws_clientcredential.h** and edit the folowing
- ![open_aws_clientcredential](https://user-images.githubusercontent.com/41168224/160010829-7975ba75-b4e6-43e7-bc99-d87f38441925.png)

```
#define clientcredentialMQTT_BROKER_ENDPOINT         "xzy-ats.iot.us-east-2.amazonaws.com"
#define clientcredentialIOT_THING_NAME               "IOT_THING_NAME"
#define clientcredentialWIFI_SSID                    "MySSID"
#define clientcredentialWIFI_PASSWORD                "MyPSWD"
```

- Build the projects
- Go to **STM32_AWS_QuickConnect** and folow the [readme.txt](https://github.com/SlimJallouli/X_CUBE_AWS_2.2.1_QC_Patch/blob/main/STM32_AWS_QuickConnect/readme.txt)
