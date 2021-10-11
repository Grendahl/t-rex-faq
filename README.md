# T-Rex FAQ


## How do I start mining?
Before you can mine, you need a crypto wallet. [MetaMask](https://metamask.io/) is easy to use and works in your browser and on your phone.

The next thing you will need is a pool. There are several example .bat files in your T-Rex folder that connect to reputable mining pools.

The simplest way to get started is to edit one of the ethereum .bat files in the T-Rex folder and replace the address in there with the receive address from your wallet for the currency you are mining. Then, save and run the .bat file to start T-Rex.

## What should I mine?
Generally speaking, you should mind the most profitable coin(s) available to you at the time. Visit [WhatToMine](https://www.whattomine.com/) and plug in your numbers to see what makes sense for you.

## I have been mining for hours now, but there is nothing in my wallet, is that normal?
Yes, that is normal. Depending on your hashrate, it will take you a few days or even weeks before you hit the minimum payout amount and the pool sends it to your wallet. 

Typical minimum payout threshold values on most ETH pools is .1 ETH. Some pools like [Ethermine](https://ethermine.org) have lower minimums, but the payout is on a different layer than mainline ethereum, so there's more work for you to do to get your profits.

## What CUDA version should I use?
* CUDA 11 is for 30xx series cards (3060/70/80/90)
* CUDA 10 is for 10xx, 16xx and 20xx series cards 

## Where do I find the best OC (overclock) settings for my GPU?
Visit [WhatToMine](https://www.whattomine.com/) and move your mouse over your graphics card. A tooltip will appear showing some settings that should get you started.

Note, when there are two memory values listed, the lower one is for Windows, and the higher one is for Linux. Do not use a linux memory setting in Windows.

The  best thing to do is to learn how to OC for yourself, per card and algo combination that you're mining, and one of our discord community members has a couple **great** videos on how to do just this!
* https://www.youtube.com/watch?v=7JGcQLgV5Gw
* https://www.youtube.com/watch?v=0F4xxcCAJVI

Go watch those, and follow along.

If you'd like to monitor your card for errors while you perform your overclock, open a CMD window and send the command ```nvidia-smi dmon -s pucvmet``` and watch the appropriate columns for errors.

## Why does my hashrate go lower when I keep increasing my --mclock value?
It's ECC memory. If it is producing errors, it has to fix them, which costs performance.

It's doing exactly what it should do. You can see the errors by opening a CMD window and send the command ```nvidia-smi dmon -s pucvmet``` to verify.

## How do I add backup pools?
Just add more pool sections (-o <pool info>) to your .bat file.
Example: ```T-Rex.exe -a ethash -o stratum+tcp://us1.ethermine.org:4444 -o stratum+tcp://us2.ethermine.org:4444 -o stratum+tcp://eu1.ethermine.org:4444```
  
Alternatively, you can add them in the WebUI if you are using a config file.

## How do I run T-Rex as an administrator?
There are several methods, but the most common way is to right click the T-Rex.exe file, select Properties, select the Compatibility tab, and check the Settings box for "Run this program as an administrator", then click OK.

## Where can I see WebUI for my miner?
Open http://127.0.0.1:4067/ (or [localhost](http://localhost:4067)) in a web browser on the mining machine.

## How do I see the T-Rex WebUI from another computer or phone on my local network?
If you cannot see your T-Rex WebUI from another computer on your local networ, it is most likely due to a firewall issue on the computer doing the mining. 
  
To open the default port (TCP port 4067) T-Rex uses for incoming connections, follow the instructions below.

**Windows:**
1. On the miner, go to Start > Run and type firewall.cpl to open the Windows Firewall window.
1. Click on the “Advanced Settings” link on the left pane. The Windows Firewall with Advanced security window opens.
1. Click on the “Inbound Rules” option.
1. On the right pane, click on “New rule”.
1. Under “Rule Type” select the option “Port” and click next.
1. Select “TCP” and “specific local ports” options.
1. Enter 4067 in the specific local ports box and click next.
1. Select the option “Allow the connection” and click next.
1. Click next. (leave the three boxes checked)
1. Enter T-Rex in the Name field and click Finish.

**Linux:**
1. From a terminal window do: ```sudo ufw allow from any to any port 4067 proto tcp``` 
1. To verify the rule was added correctly, do: ```sudo ufw status```

## What do the lines on the graph mean?
The newer versions of T-Rex have both a mouseover tooltip and a key at the bottom to show what the colors mean.
  
In older versions that don't have these features, grey is power, blue is hashrate, red is average power, and green is average hashrate.

## What intensity or kernel should I use?
T-Rex will run a benchmark when it's started and pick the best settings to run at. If you are using an external application to overclock your card(s), make sure you apply your overclock settings before you start T-Rex. If you're using T-Rex to overclock, it will do so before benchmarking.
  
If you experience hashrate drop between releases make sure that the miner selects same kernel. If kernel differs for the new version then set proper kernel manually by adding a --kernel parameter to the T-Rex startup arguments.

## How do I run a benchmark?
For Ethereum, you can start T-Rex with ```T-Rex.exe -a ethash -B --benchmark-epoch 393``` and it will give you more reports on how fast it's working. This is great for tuning your cards. 

## What is the difference between --lock-cclock and --cclock?

* --lock-cclock sets the core clock to an absolute value
* --cclock is an offset (+/-) from what the clock runs at normally 
* --lock-cclock manages power to keep the core clock where you set it
* --cclock does not manage power, so you would need to use the --pl setting to do that

## Windows says my GPU usage is very low, is this normal?
Yes, T-Rex uses CUDA to work with your GPU so Windows task manager doesn't properly report useage.

## Will validating shares influence my hashrate?
Yes, it can increase the number of stale shares your miner submits, especially if you have a slower network connection.
  
If invalid/rejected shares are a concern, you can set the --validate-shares option and look at the stats for few days.

If you have no invalid shares then your GPUs are stable and there is no need to use the share validation argument, since it is primarily intended to determine which of your gpus are not stable or working well. 

## What are error codes 15 and 999?
These errors usually indicate hardware related problems (risers, power supply, cabling etc.), see more details at: https://www.cryptoprofi.info/?p=5519

## What is the "instance wasn't validated" error? 
Right after the miner start there must be an internet connection to the developers server for miner validation. If you set firewall rules to restrict outgoing connections this can be the reason of the problem. 

## Antivirus alerts (miner shows T-Rex.exe not found error in red)
In order to protect the miner from reverse engineering attacks, the binaries are packed using a third-party software which mangles the original machine code. As a result, some antivirus engines may detect certain signatures (false positives) within the executable that are similar to those that real viruses have. 
  
Binaries which are taken from the official site https://trex-miner.com/ are completely safe. 
  
In any case, it is advisable not to use any cryptocurrency miners on the computers where you store your sensitive data such as wallets, passwords, etc.

## How do I verify miner authenticity?
After you've downloaded the miner archive from the links in releases, it's advisable to verify that its checksum matches the one listed in the release message.

**Windows Powershell:**
```Get-FileHash <PATH_TO_TREX.zip> -Algorithm SHA256 | Format-List```

**Windows CMD:**
```certutil -hashfile <PATH_TO_TREX.zip> SHA256```

**Windows 7-zip:**
Right click the downloaded zip file, click on "CRC SHA", then select "SHA-256" to get the checksum of the file

**Linux:**
```sha256sum <PATH_TO_TREX.tar.gz>```

## What does the red (!) mean?
After generating a DAG the miner computes its checksum. (!) next to it indicates that the checksum is invalid for the current epoch, and the DAG buffer is corrupted. 
  
The most common cause for this is excessive memory overclock. If the DAG buffer is corrupted, the affected GPU may produce invalid shares which will reduce your effective hashrate. 
  
Sometimes invalid shares percentage is very low and can be ignored, otherwise lower your memory overclock until (!) no longer appears.

## High CPU usage
If you experience high CPU usage by T-Rex miner process on Windows and your NVIDIA drivers are 471.11 or newer, the most likely cause is the "Hardware-accelerated GPU Scheduling" feature. 
  
To disable it, go to Start -> Settings -> Display -> Graphics settings, and turn it off.

## Why can't I save settings in the web gui?
You probably don't have a config file in the T-Rex directory, or you forgot to launch T-Rex with the -c (--config) option.

## What are the red numbers behind the R:?
That's the percentage of rejected shares. 
  
This is often an issue with your OC settings being too aggressive, causing the card to be unstable.

## How do I create an API Key?
--api-generate-key does not automatically append/edit the JSON at the current moment, in the meanwhile we have to do it manually.
1. Open a CMD window and navigate to the T-Rex directory.
1. enter: ```T-Rex.exe --api-generate-key YourDesiredWebGuiPassword```
1. Another CMD window will open with your API key in it. Copy this key and use it in your .bat or config file as the value for the --api-key setting.
1. Run T-Rex as usual, navigate to http://127.0.0.1:4067, enter the password you used to create the key, and enjoy!

### OR
Create a bat file in your T-Rex directory, paste this code into it, run it, and use the generated key in your .bat/config file.
```
<@echo off
set /p password=Choose a password for your T-Rex api-key:
cls
echo Your api-key will be shown in a new window.
echo Highlight and right click it to copy the key.
echo Once it has been copied you may close that window.
echo.
echo.
pause
start T-Rex.exe --api-generate-key %password%
exit
```

## How do I use an API Key once I've created it?
### .bat file:
Add ```--api-key YourLongApiKeyGoesHere``` to your arguments, save, and run. 
### config file:
Put your API key in the empty quotes behind the ```"api-key" : "YourLongApiKeyGoesHere",``` setting, save, and run.
                                  
When you load the web gui, it will ask you for your password. Enter the same password you used when you generated your api key.

## How does the DEV Fee work?
The miner automatically mines to the developers wallet for X/100 minutes, depending on what the fee is. 
Currently, the dev fee for ETH is 1%, so the miner mines for you 99 out of 100 minutes, and for the devs that remaining minute.

## How do DEV FEES work when dual mining?
Since it's only 30% of eth, we've set the fees to whatever they are for the second algo, i.e. 2% for dual with erg and cfx, and 1% for dual with rvn - the miner tells that at start up. 

Initially the idea was to set them to 1% but that opens up a "hack" where you set LHR 10 and pretty much mine erg or cfx with 1% instead of the usual 2% set for those algos. The fees may be reviewed (= decreased) in future releases however.

As for the way they are taken, it's no different to single mode, T-Rex mines the dev fee to the dev wallet during dev fee sessions in dual mode too.

## What do the temperature numbers in T-Rex mean?
This depends on the GPU, and what it exposes to the Nvidia driver.

T-Rex reports what it can see, in this order of preference:
* GPU and memory temp
* GPU and hotspot temp
* GPU temp only

Do not get confused between hotspot and memory temps. Hotspot temp is the highest temperature seen on the GPU die, and has nothing to do with memory temps.

GDDR6 has no temp sensors, and therefore there is no way for any tool to read the temps, while GDDR6X does have temp sensors, so those cards will show GPU and memory temps in T-Rex.

## Why can't I see memory temperatures in T-Rex?
You can only see things that the card exposes to the Nvidia driver, which is the fault of Nvidia, not T-Rex.

T-Rex simply uses the dative NVAPI functions.

## What temps should I be running on my gpu/vram?
That all depends on the silicon your GPU has.

For cards with GDDR6/6X vram, it is generally recommended to stay below 95C on memory junction temps which is shown as the second temp value in T-Rex.

For cards with GDDR6X vram, this is a good resource:
https://www.youtube.com/watch?v=ph4_Sr8YNXI

## How does memtweak work?
Memory tweak mode works similar to ETHlargementPill. It is supported on Pascal GPUs with GDDR5 or GDDR5X memory only. 
       
See the readme file for instructions on how to use the --mt parameter.

## What is LHR?
LHR (Lite Hash Rate) is something Nvidia came up with as a way to try to get graphics cards into the hands of gamers instead of miners. It is a built in limit when the card detects that it is mining ETH that limits the hashrate to 50% of the cards capability. 

T-Rex has found a way to get around this 50% barrier, and allows mining ETH at up to 70% of the cards capability. 

## What cards are LHR?
All RTX cards manufactured after mid-May of 2021 are LHR cards.
The two exceptions to this rule are:
* The RTX 3090 is not LHR
* If you have a Rev.1 3060 with the 470.05 driver on Windows it will not detect as LHR.
You can use GPU-Z from TechPowerUp to see if your card has a LHR GPU, by looking in the GPU field of the main tab of the application.

**LHR SKU Identification:**

3060 models:
* All 3060 models are LHR, no matter their SKU. (See exception above for Rev.1 cards)
           
3070/3080 models
* ASUS – LHR will be marked as version 2 or higher (ex - ROG Strix GeForce RTX™ 3070 V2)
* MSI – LHR will be marked along with the SKU (ex - 3070 GAMING TRIO PLUS 8G LHR) just like ZOTAC
* EVGA – LHR will be marked along with the SKU as “KL” (ex - 8GB GDDR6 08G-P4-3080-KL)
* GIGABYTE - LHR will be marked as version 2 / rev. 2.0 or higher
* ZOTAC - LHR will be marked along with the SKU (ex - RTX 3080 Trinity LHR or ZT-A30800D-10PLHR)

## What is LHR unlock dual mining mode?
You can now mine ETH (~30% of full speed) and other coins (~70%) simultaneously with LHR cards using their full potential.
Available combinations along with memory requirements:
* ETH+ERGO (8GB+)
* ETH+RVN (8GB+ on linux, 10GB+ on windows)
* ETH+CFX (10GB+)
See https://github.com/trexminer/T-Rex/wiki/LHR on how to set it up.
WebUI is not updated yet to reflect second algo stats in dual mode, but will be in future.

## Why are some of my config.json settings not working?
If you specify any commands in your batch file aside from --config conf.json you will not be able to change those you do specify beyond that.
       
ie: ```--config conf.json --api-key XXXX``` will allow you to change every value and save them to conf.json except for a new API key when you try to change the password via the WebUI. 

## Why does --autoupdate not work?
It only works for T-Rex 0.23.1+. There was a breaking change in 0.23.0 so auto updates was disabled for any version older than that.
       
**IMPORTANT!** If you are running a version older than 0.23.0, be sure to remove your OC settings before updating! The cards will be numered/logged into a different order so your OCs will end up on different cards than you intend. You can reapply them after update has been completed.

## How do I pause a miner?
In the WebUI, click the name of the GPU at the bottom of the main page, and then click the pause icon.

### Other options:
**Windows command (CMD):**

Open a command window and use this command (use your own IP and password)
```
for /f usebackq^ tokens^=4^ delims^=^" %a in (`"curl -s http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE"`) do @echo %a && curl "http://IP_OF_RIG_HERE:4067/control?sid=%a&pause=true"
```
  
**Windows .bat to pause T-Rex:**

Create a .bat file containing the following lines and run it.
```
:: bat to pause T-Rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=true")
pause
```
  
**Windows .bat to unpause T-Rex:**

Create a .bat file containing the following lines and run it.
```
:: bat to unpause T-Rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=false")
pause
```
  
**LINUX Bash:**
```
curl -s "http://IP_OF_RIG_HERE:4067/control?sid=`curl -s 'http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE'|cut -f4 -d'"'`&pause=true"
```

## I'm getting a Code 6:
Code 6 memory tweak errors usually points to a driver problem.
                                                                                                                                                  
* Use something like DDU (DisplayDriverUninstaller) to fully remove all Nvidia drivers
* Restart the system 
* Install the new driver directly from the Nvidia website
* Restart the system again
                                                                                                                                                  
Code 6 BusID errors almost always point to a power/riser issue.
