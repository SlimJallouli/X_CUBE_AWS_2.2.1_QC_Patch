# X_CUBE_AWS_2.2.1 Quick Connect
Prepare [X-CUBE-AWS 2.2.1](https://www.st.com/en/embedded-software/x-cube-aws.html) For Quick Connect using the [B-L4S5I-IOT01A](https://www.st.com/en/evaluation-tools/b-l4s5i-iot01a.html) board

## Prerequisite
**[STM32CubeIDE](https://www.st.com/stm32cubeide)**
- Make seure to use rev 1.8.0

**[STM32CubeProgrammer](https://www.st.com/stm32cubeprog)**

**[Python](https://www.python.org/).**

- NOTE: When installing Python make sure to install pip by selecting pip under Optional Features
-	NOTE: When installing Python make sure to select 'Add Python to the Path' during installation.
- You need to install pyserial and boto3

```
pip install pyserial
pip install boto3
```

**[Create an IAM user in your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)**
- You need the **Access_Key** and **Secret_Key**. ***(Keep them safe and don't share)***

**Wi-Fi network**
- You need 2.4 GHz

**[B-L4S5I-IOT01A](https://www.st.com/en/evaluation-tools/b-l4s5i-iot01a.html) board**

***NOTE: This was tested on Windows 10 only***

## Get the firmware packs
- Download and extreact [X-CUBE-AWS 2.2.1](https://www.st.com/en/embedded-software/x-cube-aws.html)

- Clone the repo in your **STM32CubeExpansion_Cloud_AWS_V2.2.1** directory

![X_CUBE_AWS_2 2 1_QC_Patch](https://user-images.githubusercontent.com/41168224/160009472-25c10564-b7f2-4365-a5bb-6e4496d480b2.png)

## Apply the patch
- Navigate to **X_CUBE_AWS_2.2.1_QC_Patch**
- Apply the patch
 
```
python .\apply_patch.py
```

<img width="1025" alt="run_apply_patch" src="https://user-images.githubusercontent.com/41168224/160037873-c038bc95-ef63-41e6-a002-916cb34d5220.png">

## Open the projects
- Open [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) new work space

- Click **Browse...**

<img width="432" alt="cube_ide_browse" src="https://user-images.githubusercontent.com/41168224/160032757-5255098b-a126-4717-bcc7-72d5a55721bc.png">

- Create new directory

 <img width="426" alt="cube_ide_crate_dir" src="https://user-images.githubusercontent.com/41168224/160032782-9ed1182b-4220-4f53-885c-8f79e2449535.png">

- Select the new directory
- Click **Launch**

- Close the **Information Center**

![information_center](https://user-images.githubusercontent.com/41168224/160014723-d65da8b6-dc9b-405d-8c0b-19bdd112a4a2.png)

- click **Import projects** 

 ![import_project_1](https://user-images.githubusercontent.com/41168224/160014837-5a3b7527-eccc-4b69-a283-079a95c8cd7b.png)

- Import the projects present in the **\Projects\B-L4S5I-IOT01A\Applications** directory

<img width="919" alt="cube_ide_select_folder" src="https://user-images.githubusercontent.com/41168224/160032821-99b75e95-b4dd-4706-9290-63b86987e14e.png">

- Click **Finish**
![import_project_2](https://user-images.githubusercontent.com/41168224/160015124-eb12137d-14f8-4fa2-9691-0bda62cbd4a1.png)

## Configure and build the projects

- Open **aws_clientcredential.h**. This is how you find it
 
![open_aws_clientcredential](https://user-images.githubusercontent.com/41168224/160010829-7975ba75-b4e6-43e7-bc99-d87f38441925.png)


![open_declaration](https://user-images.githubusercontent.com/41168224/160021076-87920f35-59e8-4706-abec-53f098ff4094.png)

- Get your enpoint from AWS IoT Core. You find it under ***Settings***

![endpoint](https://user-images.githubusercontent.com/41168224/160027913-4240a649-f2e1-4e44-bcee-15feb07700a3.png)

- Edit **aws_clientcredential.h**
```
#define clientcredentialMQTT_BROKER_ENDPOINT         "xzy-ats.iot.us-east-2.amazonaws.com"
#define clientcredentialIOT_THING_NAME               "IOT_THING_NAME"
#define clientcredentialWIFI_SSID                    "MySSID"
#define clientcredentialWIFI_PASSWORD                "MyPSWD"
```

![aws_clientcredential_2](https://user-images.githubusercontent.com/41168224/160016188-eac884e8-1d48-4c34-8da7-a0d82b747abf.png)


- Save your changes
- Build the projects in the following order:
 
> 1- STSAFE_Provisioning
> 
> 2- 2_Images_SECoreBin
> 
> 3- 2_Images_SBSFU
> 
> 4- aws_demos

## Run the Quick Connect script
- Switch to ***STM32CubeExpansion_Cloud_AWS_V2.2.1\STM32_AWS_QuickConnect\Scripts*** directory

![STM32_AWS_QuickConnect](https://user-images.githubusercontent.com/41168224/160022982-bb8a70a8-86e4-4ef6-947a-cc4e9b866fa6.png)

- Edit **Config.txt**

![config_txt](https://user-images.githubusercontent.com/41168224/160041842-39f315db-0b87-4ed5-9c55-7ae04a644144.png)

![config](https://user-images.githubusercontent.com/41168224/160042184-c9af15c8-585a-47e0-84c1-0a0465a1ad52.png)

***NOTE: The Wi-Fi SSID and PASSWORD are not used in this version of Quick Connect***

***NOTE: Region should be the same as in the enpoint (us-east-2) as in the example below***

```
#define clientcredentialMQTT_BROKER_ENDPOINT         "xzy-ats.iot.us-east-2.amazonaws.com"
```

***More details can be found in [readme.txt](https://github.com/SlimJallouli/X_CUBE_AWS_2.2.1_QC_Patch/blob/main/STM32_AWS_QuickConnect/readme.txt)***

- Make sure your board is connected to your computer over USB. Make sure to use the ST-Link USB port

- Execute the **Quick Connect** script

```
python .\STM32_AWS_QuickConnect.py
```

<img width="855" alt="run_qc" src="https://user-images.githubusercontent.com/41168224/160037963-737b9363-d5b3-4b57-b0ba-78dae16cd65a.png">

## Check your device in AWS IoT Core

![check_device_iot_core](https://user-images.githubusercontent.com/41168224/160038221-6b8f3d7b-9d2a-45e2-b265-21ea7167b657.png)
