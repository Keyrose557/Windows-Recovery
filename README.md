# Windows Recovery Solution

Found this issue. Here are my notes on the fix. 

![issue](/media/issue.JPG)

## Windows Media Creation

I utilized my trusted Windows Recovery USB tool. 

### Bios

Entering the BIOS I used `esc` or `del` for my hardware. 

Keep in mind getting into the BIOS, some hardware could also use `f2` or `f12`

![boot](/media/boot0.JPG)

Once in the BIOS we want our hardware to run or `boot` from our recovery usb stick. 

![boot](/media/boot2.JPG)

![boot](/media/boot1.JPG)

Once we have updated our boot option to our desired tool. We can Save & Exit. 

Windows should boot up now as shown below

![sysrec](/media/rprwin.JPG)

- Select `Repair my pc` > `Troubleshoot`

![sysrec](/media/sysimg.JPG)

Here we can see the options presented. I prefer to utilize System Image Recovery because its fast and I know it will solve the issue.
 
However I did include notes on the other options on how successful or unsuccessful it was at solving the issue.

## System Image recovery

**Requisites**:

- Windows Recovery USB
- System Image File
- External Storage (to store the system image file)

**Outcome**: ~11 min recovery time

Select Repair my PC > System Image Recovery

![sysrec](/media/sysimg.JPG)

**Warning** if you manage multiple images on the same external drive its easy to make a mistake here, loading the wrong image.

Sometime Windows wont recognize the images if the drive is not formatted correctly. I tend to use multiple drives and I remember that being an issue for me.

**Verify** before moving on, your desired image 

Select `next`

![sysrec](/media/sysimh2.JPG)

Select `next`

![sysrec](/media/sysimg3.JPG)

 Select `finish`

![sysrec](/media/sysimg4.JPG)

Final Confirmation message, Select `yes`

![sysrc](/media/sysimg5.JPG)

This will start the process and it took ~11 min to complete on an SSD

![sysrec](/media/sysrec.JPG)

Once the process completes the workstation will reboot and boot up the windows image.

## Unsuccesful Attempts 

I was curious if the options below would have fixed the issue, they didnt.

### Startup repair option

Did not work

![rpr](/media/rprwin2.JPG)

### Command Prompt

I issued the command below and got some helpful insight of the issue. However despite a reboot, I still got the same Windows Failed to Start issue during the boot process. 

```bash

sfc /scannow

```

![cmd](/media/cmd1.JPG)

- step taken: `reboot`

So I tried this again but this time I wanted to investigate the logs and found something weird.

Using the commands, after running `sfc /scannow`

```bash

notepad C:\Windows\Logs\CBS\CBS.log

```

Notepad opened but it was unable to find the specified path...

Okay lets look for our drive than. I used the command below

```bash

diskpart
list vol

```

![ssd](/media/IMG_6608.JPG)

This is what I thought what was weird. Windows is not recognizing our SSD. This didnt make sense to me... If the boot loader is showing up in the bios it isnt a hardware fault.

**Volume 0 and 1** is the HHD that I use for backups and diaster recoveries

**Volume 2** is the WinRE USB stick

Maybe its a windows quirk... Im not entirely sure but for the sake of fixing the issue in a timely manner I decided to shift focus back to the solution versus the problem.




