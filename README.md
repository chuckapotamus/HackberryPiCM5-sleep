# Hackberry Pi CM5 Sleep
### Modified uConsole code

Found on the uConsole forums originally, I wanted to see if I could get this working on the Hackberry Pi with a CM5 module by Zitao. Mostly working but has a couple of quirks to work out due to the Hackberry's different build. 
Issues still being worked out are as follows:

- Screen "blanks" properly but leaves lines on display which cause bad burn-in when the panel isn't given a signal.
- Max clock speed drops to lower end but does not follow the config file's setting. Does seem follow any speeds set in the boot/firmware/config.txt file.

The rest below is from the original project for posterity. I'm including a changes_dateXXX.txt file to show what I've changed explicitly alongside a *.original file to show the original script. 
Please let me know if there's something I missed or didn't understand from the original script!

######

# uConsole-sleep
### uConsole Sleep service package

This service is built on Ubuntu 22.04 and Python.

It detects power key events to turn the screen on and off. Initially, I used a polling loop for event detection, but to reduce CPU load, I switched to using epoll.

Whenever the screen turns off for any reason (e.g., screensaver, desktop lock, sleep mode), 
the service detects the screen-off state and lowers the CPU’s maximum frequency to the minimum while also turning off the built-in keyboard’s power and wakeup trigger.

(I also tried changing the CPU governor to `powersave`, but I noticed a slight delay when switching.)

Similarly, I initially used a polling loop to detect screen-off events, but to reduce CPU load, I switched to using inotify.

The service consists of two background processes:

* **sleep-remap-powerkey**
`/usr/local/bin/sleep_remap_powerkey`
Detects power key events and controls the screen power.
* **sleep-power-control**
`/usr/local/bin/sleep_power_control`
Manages power-saving operations based on screen status.

**More Details**
[on forum.clockworkpi.com](https://forum.clockworkpi.com/t/uconsole-sleep-v1-2/15612?u=paragonnov)


<a href="https://www.buymeacoffee.com/paragonnov" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-red.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
