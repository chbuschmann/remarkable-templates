# SSH
Before we start, there is a piece of software that does all of this. Its called RCU. It is quite cheap and good. Just buy it and rejoice. 
https://www.davisr.me/projects/rcu/

If you want to do it on your own, here is how:

## Step 1
First we need to enable access via SSH. This is partially described here: https://support.remarkable.com/s/article/Developer-mode but without handrails. Lets spell it out step by step:
- We need to enable Developer Mode:
`Settings -> General -> Software -> Advanced`

- **IMPORTANT!**: This will wipe the tablet to factory, _all files will be deleted!_
If you have your files synced via their cloud subscription, your files will sync after you re-pair the device. Same process as when you first paired it to my.remarkable.com
Ergo: Make sure you either have your device and documents either backed up, synced, or simply blank.

- After the obligatory wait and re-pairing you need to find your device IP and password for root access:
`Settings -> General -> Help -> About -> Copyrights and licenses`

- Make note of the IP and password, and remember this command:
`rm-ssh-over-wlan on`

- Connect your tablet via usb to your workhorse of choice, i'm on macOS so adjust your workflow as needed.
Open your terminal and write: `ssh root@[IP]`
Mine turned out to be: `root@10.0.0.223`

- Enter the password when prompted.

Et voila! Your terminal will display something like this: `root@imx8mm-ferrari:~#` 
Ferrari is the internal codename of the operating system, or something similar.

## Step 2
We are insided the lions den, but we need to do a few more steps:
- First we enable ssh access wireless. This way we dont need the USB connection. 

`rm-ssh-over-wlan on`

You can now access your tablet wirelessly. 

- Then we need to make the system writable with: `mount -o remount,rw /`

The `mount -o remount,rw /` command changes the file system’s state to read-write, allowing you to write to the file system.
	•	`-o remount`: This part of the command tells the system to “remount” the file system without unmounting it first.
	•	`rw`: This option sets the file system to read-write mode.
	•	`/`: This refers to the root directory, meaning you’re remounting the root file system with read-write permissions.

Now we have access to the system and can copy, paste and delete to our hearts content. 

## Optional: Cyberduck
If you know your way around the terminal, ie vim/nano and scp you are all good from here. The files you want are in: `/usr/share/remarkable`.

If you're like me and find navigating the terminal all by text a hassel rest assured, there are ways around this. Cyberduck is my weapon of choice. It gives you a GUI that lets you browse files and folders like on your desktop.

Download Cyberduck from https://cyberduck.io, open a new connection, choose SFTP and enter your ip, user (`root`) and password. Navigate to `/usr/share/remarkable` and be careful. You can delete files, and there is no Bin to save you.

## Templates
- You have to have a .svg file, and you need to edit the templates.json. When i was using RCU it also created a .png but I tried with just the .svg and it worked fine.

- Copy your new template(s) into `/usr/share/remarkable/templates`.
-With a text editor edit the .json as follows:

This is the three last entries of my .json to give you an idea of the formating. This first of the three is one of the factory templates, the two last is my own. 

```
        {
            "categories": [
                "Grids"
            ],
            "filename": "P Hexagon small",
            "iconCode": "\ue98c",
            "name": "Hexagon small"
        },
        {
            "categories": [
                "Creative"
            ],
            "filename": "4-bar",
            "iconCode": "\ue977",
            "landscape": false,
            "name": "Sheet Music 4 Bar"
        },
        {
            "categories": [
                "Creative"
            ],
            "filename": "music-blank",
            "iconCode": "\ue977",
            "landscape": false,
            "name": "Sheet Music Blank"
        }
    ]
}
```

The iconCodes can be found here: https://www.reddit.com/r/RemarkableTablet/comments/j75nis/reference_image_template_icon_codes_for_23016/

- After this you need to either restart you tablet, or just run this in your terminal:
`systemctl restart xochitl`

`xochitl` is the operating system, as far as i understand it, and this command simply reloads it. Lots faster then a full system reboot.

## Splash screen

There are several splash screens to edit. The one I customized was `suspended.png`. The dimensions is as follows:

```
*reMarkable Paper Pro*
Resolution: 2160 x 1620 pixels
Pixel Density: 229 PPI
Aspect Ratio: 4:3
Colours: 20 000
```

Drag suspended.png to a folder on your computer and rename it to something clever, like `suspended_bak.png`
Create/edit/midjourney your shiny new splashscreen with an aspect ratio of 3:4 if you want it to be oriented in portrait, 1620x2160px, 300dpi, all the colours you want, name it `suspended.png` and drag it into `/usr/share/remarkable`. Cyberduck will ask you what to do, you want to overwrite the original. 

And thats it. Press the top button and behold your new splash screen.

## End of the line
There are ofcourse caveats, like after an update everything is put back to factory, but you now know what to do. I keep my tablet in dev mode all the time, but if you store sensitive data it is probably not a great idea. 

Good luck!

	Buschmann, 18. feb 2025
