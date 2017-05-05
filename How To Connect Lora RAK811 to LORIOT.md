# How To Connect Lora RAK811 to LORIOT
## 1.Introduction
This document mainly gives a detailed introduction about how to connect RAK811(Lora) to LORIOT.
RAK811 Low-Power Long Range LoRa Technology Transceiver module, provides an easy to use, small size, low-power solution for long range wireless data transmission. 
First, The RAK811 module complies with the latest LoRaWAN Class A & C protocol specifications, it is simple to access LWPA IOT platforms, such Actility etc. Second, it also support Lora Point to Point communications, this function can help customers implement their own private long range Lora network fast.
Module integrates semtech SX1276 and stm32L, offer user an serials At commands with UART Interface .It is easy to accomplish their applications, such as simple long range sensor data applications with external host MCU, low-power feature is suitable for battery applications.
##### I will introduce the following four parts in detail:
##### (1)Registered Account;
##### (2)Add Gateway to LORIOT;
##### (3)Upgrade the Firmware of the Gateway;
##### (4)Add RAK811 to LORIOT;

<br>

## 2.Registered Account
If you wanted connect the RAK811 to LORIOT,you need to register an account on LORIOT. Its website is [https://www.loriot.io/](https://www.loriot.io/). Now,please follow the step below to register.
Please click the URL mentioned above,or copy and paste this URL and open with browser;
#### Step 1: Open this website;
#### Step 2: Click ”LOG IN”;
![](http://i.imgur.com/7IkImOv.png)

#### Step 3: Pick a server below based on your geographic location preference, at here I am choose “Shenzhen,China”and click;
![](http://i.imgur.com/hQUghpE.png)

#### Step 4: Click “Register”and starting to registration;
![](http://i.imgur.com/WbRKPTO.png)

#### Step 5: You will see a registration form, fill in the form as required. After filling,click “CREATE A FREE ACCOUNT”and complete registration;
![](http://i.imgur.com/dY7KjVw.png)

#### Step 6: Wating a moment you will received a email from LORIOT,it shown that you register account successfully.and click on the link in the email activate your account. 

<br>

## 3.Add Gateway to LORIOT
Please log in to your account and follow the steps below, Here I use MultiTECH gateway device to demonstrate:
#### Step 1: Log in your account, Click“Home”, Go to your Dashboard, then click “Gateways”;
![](http://i.imgur.com/sRzVaob.png)

#### Step 2: Click “Add gateway”;
![](http://i.imgur.com/khM2XGC.png)

#### Step 3: Choose the gateway what you used;
![](http://i.imgur.com/2kb2Iwa.png)

#### Step 4: According to the actual situation of the gateway equipment information, like “Card”, “eth0 MAC address”, “Gateway location”;
![](http://i.imgur.com/VSusw1f.png)

#### Step 5: Click “Register MultiTech Conduit mLinux gateway”, finish register;
![](http://i.imgur.com/yUOVjVt.png)

#### Step 6: After step 5, we have completed the addition of the gateway, but it is still in an inactive state. In the next chapter, I'll show you how to update the firmware of the gateway to activate it.
![](http://i.imgur.com/RWademG.png)

<br>

## 4.Upgrade the Firmware of the Gateway

To activate our gateway, to LORIOT, we need to download the firmware and flash the gateway. But how to set our gateway?
#### Step 1: Open “Dashboard”- “Documentation”- “Setup guides”, select the appropriate installation guide based on your own gateway model and click on;
![](http://i.imgur.com/rBTaTeY.png)

#### Step 2: Complete the firmware upgrade according to installation guide;
![](http://i.imgur.com/aZWQLIT.png)

#### Step 3: Refresh Gateways page, You can see that the gateway is already active;
![](http://i.imgur.com/BHLih2w.png)

<br>

## 5.Add RAK811 to LORIOT
In this part, I will use WisNode-Lora EVB to demonstrate how to add our LoRa RAK811 module to LORIOT;
![](http://i.imgur.com/40lcrzy.png)
###                          RAK WisNode-Lora EVB

#### Step 1: Open “DashBoard”- “Applications”- “SampleApp” - “Enroll device”, then fill in “Device EUI”, and  click on“Enroll OTAA/ABP device”, start to add RAK811 Lora module. 
![](http://i.imgur.com/dzr2XNR.png)

Device EUI: Enter the DevEUI for your device. This ID should come with the information included with your device, or can be found in the device use at+get_config=dev_eui.

#### Step 2: Click on“Device”;
#### Step 3: We have completed the add the RAK811 Lora module, but it is still in an inactive state ;
![](http://i.imgur.com/9F2TsI2.png)

#### Step  4: Click on “Device EUI”;
![](http://i.imgur.com/GvZMAA8.png)

#### Step 5: On the page you will see the information about RAK811 LoRa module, like DevAddr, AppKey, NwkSkey, AppSKey;
#### Step 6: Use Micro USB interface to supply the module power. One end of the serial line is connected to the module, and one end is connected to the computer. Then open the Uart AssistTool, send AT command to operate the module.
![](http://i.imgur.com/8WeDfTK.png)


#### Step 7: Send the AT command to the module in the following order, make the RAK811 module join the abp;
    Boot information : Welcome to RAK811

    Send: at+mode=0                    /* SET LoraWAN work mode */
    Return: OK

    Send:at+set_config=dev_eui:60C5A8FFFE000001   /* GET Dev_EUI check if NULL ,set the enter before information */ 
    Return: OK

    Send:at+set_config=dev_addr:013F17FD&nwks_key:4CAD9901FEB8F6801D0C3BE1E9DD76D1&apps_key:F39F38D314EC5DCB0F6D55ED734F2F98
    /* SET LoraGateway dev_addr nwks_key and apps_key , big endian*/
    Return: OK

    Send: at+join=abp       /* Join abp type*/
    Return: OK
![](http://i.imgur.com/1v1l2ou.png)

#### Step 8: After join abp, then can use the following AT command send data to LORIOT, then refresh dashboard page,we can see our Device is Active , it means our module connect with LORIOT;
    Send: at+send=0,2,000000000000007F0000000000000000 
    Return: at+recv=2,0,0  /*unconfirmed mean tx success*/
![](http://i.imgur.com/RlRbxLv.png)

![](http://i.imgur.com/eJsasuY.png)

![](http://i.imgur.com/pAuM8NW.png)



111111111





