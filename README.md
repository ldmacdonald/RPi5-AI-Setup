# Raspberry Pi 5 with AI Hat Setup

## Intro
You've just gotten your shiny new Raspberry Pi 5 AI Hat installed and are following the instructions when you start running into a bunch of issues that don't seem to make much sense.
Or is that just me?  Either way, this guide is intended to help you get through the initial setup and ready for your first project.

## Driver install

The first issue that I, and presumably you'll, hit is that the tensor board is not recognized.

The [RPi Forum](https://forums.raspberrypi.com/viewtopic.php?t=395534) indicates that the `dkms` package is a pre-requisite for hailo install, and as it resolved my issues, this seems to be correct.

```
sudo apt update
sudo apt full-upgrade
sudo install dkms
sudo install hailo-all
```

## Use dmesg to check your install
Running `dmesg` should provide some feedback if your install will work, ideally this should show some kernel messages.
```
dmesg | grep hailo
```

And then a reboot is needed to finish this phase of the configuration
```
sudo reboot
```

## Check that your hardware is recognized
With those steps out of the this way, the below command
```
hailortcli fw-control identify
```

should return something that looks like this
```
Executing on device: 0001:01:00.0
Identifying board
Control Protocol Version: 2
Firmware Version: 4.23.0 (release,app,extended context switch buffer)
Logger Version: 0
Board Name: Hailo-8
Device Architecture: HAILO8L
Serial Number: HLDDLBB243303522
Part Number: HM21LB1C2LAE
Product Name: HAILO-8L AI ACC M.2 B+M KEY MODULE EXT TMP
```
If you get to this step and there is nothing returned, you'll likely need to restart from a fresh OS install.

The latest version of the Raspberry Pi Imager should get you through this step.


## Hailo has a brand new Repo

Most of the examples that I have seen to this point use an older hailo demo repository [https://github.com/hailo-ai/hailo-rpi5-examples.git](https://github.com/hailo-ai/hailo-rpi5-examples.git).

However, there is an updated version which runs with a simple install script here [https://github.com/hailo-ai/hailo-apps](https://github.com/hailo-ai/hailo-apps).
```
git clone https://github.com/hailo-ai/hailo-apps
cd hailo-apps
sudo ./install.sh
```

After the install is done, you can run a demo with the command below.

```
source setup_env.sh           # Activate environment
hailo-detect-simple           # Start object detection
```

The demo includes a GUI, but if you're ssh'd in like I was, you'll get an output looking like this:

```
Frame count: 29847
Detection: person Confidence: 0.91
Detection: person Confidence: 0.89
Detection: person Confidence: 0.89
Detection: person Confidence: 0.88
Detection: person Confidence: 0.85
Detection: person Confidence: 0.82
Detection: person Confidence: 0.80
Detection: person Confidence: 0.55
Detection: person Confidence: 0.46
Detection: car Confidence: 0.57
Detection: car Confidence: 0.48
Detection: car Confidence: 0.47
Detection: traffic light Confidence: 0.41
Detection: backpack Confidence: 0.36
Detection: backpack Confidence: 0.31
```

You should now be good to start playing around with your new environment.

Happy tinkering!
