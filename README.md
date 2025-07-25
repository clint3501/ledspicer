# ledspicer
config files and instructions for using ledspicer with batocra v41

Figured I would pass this along considering all the positive help I have received from many colleagues when putting this all together.  Use what I am providing as is and if I forgot to properly credit a product or person my apologies in advance.

I am using LedSpicer for the LED control and all works.  In short I have successfully added led light control to my arcade system that is using RetroKnights package for light guns https://retroknightgaming.com/store/product/p_3249758 which works exceptionally well.
I am including in this description and the associated tar ball all the working files and steps to get ledspicer working with Batocera v41 matching my configuration.   

There are numerous files available on github and elsewhere with different configs all made free by a few individuals who are doing great work.  It’s a relative mess due to it being a moving target because of the multitude of hardware/emulator/rom variations everyone is using. There is no gold standard for obvious reasons. When I was putting together this information, i.e. initially trying to configure things, I was not as diligent as I should have been to identify what file I got from where.  

Here are a few key links that are worth exploring first, these were the sources I got all my information from.
•	https://github.com/MrRobot-108
•	https://github.com/meduzapat/LEDSpicer
•	https://github.com/meduzapat/LEDSpicer/wiki/
•	Discord for Ledspicer is another great source  https://discord.com/channels/1187485303313809528/1187485303766782004  (this should work or just log into discord and search for ledspicer)

When I had a few issues, I leaned in on Discord and got some great help.  If you go to Discord, there is a lot of information here regarding ledspicer and it is worth looking over it before asking any questions.

I am using an Ultimarc PacLED64 for controlling my LED buttons both of which I got from Ultimarc.   I initially attempted to get Ledspicer running using a Ultimarc Ultimate IO board.  However, I am using Batocera v41 and the Ultimate IO board when using Batocera cannot use ledspicer, there is some licensing issue with Xbox as it was later explained by Ultimarc.  In short ledspicer does not like interfacing to a led controller that is identified as a keyboard.  Therefore, I switched the LED control to the PacLED64 but kept the controller functions with Ultimate since I had it already which is a slight overkill for what I am doing.

The following is a picture of my completed arcade cabinet.

<img width="317" height="563" alt="image" src="https://github.com/user-attachments/assets/b40bb801-6c1b-4121-a359-8a48f0ee3fa9" />

The following is diagram of my control panel 

<img width="551" height="235" alt="image" src="https://github.com/user-attachments/assets/25207b03-1367-4495-93d1-8417b655a9e2" />

Here is a brief high-level system diagram of my configuration

<img width="529" height="599" alt="image" src="https://github.com/user-attachments/assets/17720458-1e95-4eab-b402-023c5804bab8" />

As several have suggested please review the ledspicer file structure and ledspicer/emitter commands both are important later if there are any issues.
Look at files provided in the tar file. You need to move them to the right directories as described below. 

Get these files ready, do not put them into Batocera just yet. You will need to activate Ledspicer first to create the requisite directories.  
However, the files you need are listed next, get them organized so you can copy when needed.

<img width="975" height="1305" alt="image" src="https://github.com/user-attachments/assets/be45093d-0ef9-49db-bd88-74b3a52c54d1" />

Install Instructions:
I got all my initial files from github and frankly I cannot remember if I got everything here from Meduzapat or Mr Robot or if it’s a combined thing.  Anyway  
1.	ledspicer.conf (hardware related)
2.	controls.ini
3.	colors.ini
4.	scripts for changing colors
5.	profiles default.xml & profile_arcade.xml
   
The desired location for ledspicer is userdata/systems/configs.

The profile_arcade.xml is loaded for any detected game (requires animation scripts).  In many of the ledspicer.conf files default.xml is called.  I decided to use profile_arcade.xml to keep a default.xml if I needed it in the future.  Use what you want for the file name just make sure the ledspicer.conf file called matches what is in the profile directory.

The ledspicer.conf file supplied is configured for my system.   This is a key file, and you may need to change this if you are usings a different LED control board or have your LEDs assigned differently than what I did. 

I had some issues with a few MAME files like defender and missile command where I had a hard time getting the color scheme to work.  The culprit was the rom name while appearing to be the same was not, so I did the rename copy the file name and use that for the profile name in the rom_ledspicer.csv to get things working the way I wanted.  I probably missed something but this brute force approach worked and I moved on.  Of course, you will need to map the MAME functions to the buttons to match the led color scheme I used or make your own.

I am also using serpentine for the moment and have been switching between gradient and serpentine for now.

I have also included the files I used which all you need to do is copy them from your drive to the appropriate Batocera directory using WinSCP.    

You will also need to use Putty to get permissions for some directories.

The following are my instructions.  I reloaded everything onto a fresh batocera load when I typed these instructions and hopefully there are no errors.

1)	Install:
Before you begin installing you need to check if ledspicer is enabled already.   Using WinSCP to navigate to the directory userdata/system/configs and check to see if ledspicer folder is present, if it is it was previous turned.  If you see ledspicer as a directory, then it was previously activated.

If ledspicer is not activated, then you will need to (2) Activate Ledspicer.If it is activated just skip the Activate Ledspicer section and go to (3) Configuring Ledspicer.

2)	Activate Ledspicer:

With Batocera running press the select button and then scroll down to 

System Settings- select this
Then go Services
In Services – activate ledspicer
Backout and then
Reset/Restart Batocera

Verify Userdata/system/configs/ledspicer is now present (with sub directories) if not repeat (1) and (2) with a shutdown. WinSCP is easiest way to check.
The ledspicer directory should have the following structure (there are just readme.txt in all the folders except umaps which is left untouched.

/userdata/systems/configs/ledspicer/
	-umaps
	-profiles
	-inputs
	-annimations
	ledspicer.conf

 3)	Configuring Ledspicer:

At this stage it’s time to configure things.
Start an instance of Putty and WinSCP.  Putty is your terminal and WinSCP is for file transfer, though you could use Putty for all this WinSCP makes life easier.

1)	Copy the following files and directories into userdata/system/configs/ledspicer replacing the files that are there.
a.	Ledpsincer.conf
b.	colors.ini 
c.	umaps
d.	inputs
e.	profiles
f.	animation (delete the readme.txt file in the original directory first)
g.	gameData.xml
h.	basicColors.xml

2) <img width="811" height="342" alt="image" src="https://github.com/user-attachments/assets/2a1b512c-39d7-4f41-9286-e33e2cc14b75" />

3)	Now go to userdata/system/configs/emulationstation and copy the scripts directory into the emulationstation directory

<img width="719" height="219" alt="image" src="https://github.com/user-attachments/assets/a26567b6-47ff-499d-9a54-e6e21e6abb7c" />

4)	Check to see that all four files transferred in the scripts directory
•	Game-end
•	Game-selected
•	Game-start
•	System-selected

5)	The directory rights should have transferred, however, to be safe open a Putty terminal and navigate to the directory
userdata/system/configs/emulationstation/scripts

<img width="707" height="277" alt="image" src="https://github.com/user-attachments/assets/06a77197-db25-4261-a7de-a6985ac7f6c0" />
6)	Run in a terminal (putty) by entering the following commands.
chmod +x /userdata/system/configs/emulationstation/scripts/system-selected/system-selected.sh
chmod +x /userdata/system/configs/emulationstation/scripts/game-start/game-start.sh
chmod +x /userdata/system/configs/emulationstation/scripts/game-selected/game-selected.sh
chmod +x /userdata/system/configs/emulationstation/scripts/game-end/game-end.sh

In discord the basicColors.xml was commented it was preloaded on install, that was not my case, so the file is in the group provided.
That’s it, at least for my configuration.

You will need to restart Batocera now (do a complete shutdown).

When you restart Batocera the led lights should respond.  You can then modify the leds as desired or just keep them as is.

Some notes:
1.	Ledspicer.conf is set up for my configuration, please note the board name used. Everything will fail if the wrong board name is used.  If you are not using a PacLed64 board then you will need to find an example to follow which I did not provide.

<devices>
		<device
			name="UltimarcPacLed64"
			boardId="1"

2.	Profiles directory has an excel sheet for configurating the button color profiles   Change the profile configuration in the excel sheet, save it to the profiles directory and then select (run) the generate.py file by double clicking it.  The generate.py will auto populate the system profiles as you want. You can change it as repeatedly until you get things the way you want them.

3.	Arcade directory (MAME profiles)– this is located in the profiles directory and there is an excel sheet for configurating the button colors of the MAME games.  The excel file is roms_ledspicer.  I modified the generate script for this do it will use the rom_ledspicer file for games and remembering it’s for games and not a system.  Easier from my viewpoint instead of hunting and pecking the game profiles or just running another instance of the system_ledspicer
4.	To change animation once set up need to modify profiles_arcade.xml file (or default.xml if you went down that path)







