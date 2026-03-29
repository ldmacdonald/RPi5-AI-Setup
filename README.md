# RPi5-AI-Setup

The [RPi Forum](https://forums.raspberrypi.com/viewtopic.php?t=395534) indicates that the `dkms` package is a pre-requisite for hailo install and this seems to be correct.
```
sudo install dkms
sudo install hailo-all
```
## Use dmesg to check your install
Running `dmesg` should provide some feedback if your install will work, ideally this should show some kernel messages.
```
dmesg | grep hailo
```

A reboot is needed to start finish the configuration
```
sudo reboot
```

## Check that your hardware is recognized

```
hailortcli fw-control identify
```

The command should return something that looks like this
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
If you get to this step and there is nothing returned, you'll likely need to start from a fresh OS install


## GitHub clone from example

In repo
```
python -m venv venv_hailo_rpi_examples
source venv_hailo_rpi_examples/bin/activate
```
