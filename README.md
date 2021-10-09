# T-Rex FAQ


## How do I start mining?
Before you can mine, you need a crypto wallet. [MetaMask](https://metamask.io/) is easy to use and works in your browser and on your phone.

The next thing you will need is a pool. There are several example .bat files in your t-rex folder that connect to reputable mining pools.

The simplest way to get started is to edit one of the ethereum .bat files in the t-rex folder and replace the address in there with the receive address from your wallet. Then, save and run the .bat file to start t-rex.

## What should I mine?
Generally speaking, you should mind the most profitable coin(s) available to you at the time. 
Visit [WhatToMine](https://www.whattomine.com/) and plug in your numbers to see what makes sense for you.

## Been mining for hours now, not seeing anything in my wallet, is that normal?
Yes, that is normal. Depending on your hashrate, it will take you a few days or even weeks before you hit the minimum payout amount and the pool sends it to your wallet. 

Typical minimum payout threshold values on most ETH pools is .1 ETH. Some pools like ethermine.org have lower minimums, but the payout is on a different layer than mainline ethereum, so there's more work for you to do to get your profits.

## What CUDA version should I use?
CUDA 11 is for 30xx series cards (3060/70/80/90)
CUDA 10 is for 10xx, 16xx and 20xx series cards 

## Where can I find OC (overclocking) settings for my GPU?
Visit [WhatToMine](https://www.whattomine.com/) and move your mouse over your graphics card. A tooltip will appear showing some settings that should get you started.

Note, when there are two memory values listed, the lower one is for Windows, and the higher one is for Linux. Do not use a linux memory setting in Windows...

## How can I add backup pools?
Just add more pool sections (-o <pool info>) to your .bat file.
Example: ```t-rex.exe -a ethash -o stratum+tcp://us1.ethermine.org:4444 -o stratum+tcp://us2.ethermine.org:4444 -o stratum+tcp://eu1.ethermine.org:4444```

## How can I run T-Rex as an administrator?
There are several methods, but the most common way is to right click the t-rex.exe file, select Properties, select the Compatibility tab, and check the Settings box for "Run this program as an administrator". Then click OK.

## Where can I see WebUI for my miner?
Open http://127.0.0.1:4067/ in a web browser on the mining machine.

## What do the lines on the graph mean?
The newer versions of t-rex have both a mouseover tooltip and a key at the bottom to show what the colors mean.
  
In older versions that don't have these features, grey is power, blue is hashrate, red is average power, and green is average hashrate.

## What intensity or kernel should I use?
T-Rex will run a benchmark when it's started and pick the best settings to run at. If you are using an external application to overclock your card(s), make sure you apply your overclock settings before you start t-rex. If you're using T-Rex to overclock, it will do so before benchmarking.
  
If you experience hashrate drop between releases make sure that the miner selects same kernel. If kernel differs for the new version then set proper kernel manually by adding a --kernel parameter to the t-rex startup arguments.

## How do I run a benchmark?
For Ethereum, you can start T-Rex with ```t-rex.exe -a ethash -B --benchmark-epoch 393``` and it will give you more reports on how fast it's working. This is great for tuning your cards. 

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

## Antivirus alerts (miner shows t-rex.exe not found error in red)
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
You probably don't have a config file in the t-rex directory, or you forgot to launch t-rex with the -c (--config) option.

## What are the red numbers behind the R:?
That's the percentage of rejected shares. 
  
This is often an issue with your OC settings being too aggressive, causing the card to be unstable.

## How do I create an API Key?
--api-generate-key does not automatically append/edit the JSON at the current moment, in the meanwhile we have to do it manually.
1. Open a CMD window and navigate to the t-rex directory.
1. enter: ```t-rex.exe --api-generate-key YourDesiredWebGuiPassword```
1. Another CMD window will open with your API key in it. Copy this key and use it in your .bat or config file as the value for the --api-key setting.
1. Run t-rex as usual, navigate to http://127.0.0.1:4067, enter the password you used to create the key, and enjoy!

### OR
Create a bat file in your t-rex directory, paste this code into it, run it, and use the generated key in your .bat/config file.
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
start t-rex.exe --api-generate-key %password%
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

As for the way they are taken, it's no different to single mode, t-rex mines the dev fee to the dev wallet during dev fee sessions in dual mode too.

## What temps should I be running on my gpu/vram?
That all depends on the silicon your GPU has.
       
For cards with GDDR6/6X vram, this is a good resource:
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
It only works for t-rex 0.23.0+. There was a breaking change in 0.23.0 so auto updates was disabled for any version older than that.
       
**IMPORTANT!** If you are running a version older than 0.23.0, be sure to remove your OC settings before updating! The cards will be numered/logged into a different order so your OCs will end up on different cards than you intend. You can reapply them after update has been completed.

## How do I pause a miner?
In the WebUI, click the name of the GPU at the bottom of the main page, and then click the pause icon.

### Other options:
**Windows command (CMD):**

Open a command window and use this command (use your own IP and password)
```
for /f usebackq^ tokens^=4^ delims^=^" %a in (`"curl -s http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE"`) do @echo %a && curl "http://IP_OF_RIG_HERE:4067/control?sid=%a&pause=true"
```
  
**Windows .bat to pause t-rex:**

Create a .bat file containing the following lines and run it.
```
:: bat to pause t-rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=true")
pause
```
  
**Windows .bat to unpause t-rex:**

Create a .bat file containing the following lines and run it.
```
:: bat to unpause t-rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=false")
pause
```
  
**LINUX Bash:**
```
curl -s "http://IP_OF_RIG_HERE:4067/control?sid=`curl -s 'http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE'|cut -f4 -d'"'`&pause=true"
```


