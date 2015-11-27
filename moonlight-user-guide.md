## 1. Introduction

**Moonlight** (formerly known as Limelight) is an open source implementation of nVidia's GameStream protocol, a protocol developed and used by the NVIDIA Shield family of products. GameStream allows a computer with a video card compatible with the GeForce Experience program to stream games to SHIELD devices, providing video and a controller to play games remotely.

With Moonlight, you can use this same protocol to stream a collection of games from a GameStream-compatible PC to any supported device, not just the SHIELD family, and play them remotely. Moonlight is perfect for gameplay on the go without sacrificing the graphics quality of a gaming computer. Moonlight also makes it possible to play PC-exclusive games on mobile devices, freeing anyone from the need to sit at the gaming computer to play.

## 2. System Requirements

### Server Requirements

For the computer that will be serving up the games (the server), the key component is having an nVidia graphics card that the GeForce Experience can use.

Practically, this means that the video card (GPU) needs to be from either the **GTX series (600, 700, 900)** or a **700M, 800M, or 900M series** GPU. (Some 600M series can manage it, but to be safe, it's better just to go with the 700 or higher series) You can find a reasonable GTX card for about $125, minus any rebates you might get from the manufacturers or who you buy the GPU from.  

In addition to that, nVidia suggests the following: (http://www.geforce.com/geforce-experience/system-requirements)

* Operating System: Windows Vista or newer, with DirectX 11 or newer installed

* A CPU of reasonable newness (Intel Pentium G Series, Core 2 Duo, Quad Core i3, i5, i7, or an AMD Phenom II, Athlon II, Phenom X4, FX, or any newer, higher speed processor from either of those manufacturers)

* At least 2GB RAM, more preferred

* 20 MB of hard disk space for GeForce Experience, plus whatever additional hard disk space requirements are needed for the streamed game or game platform client, like Steam or Desura.

* A display that can handle at least 1024x768

* A connection to the Internet to download the software.

If your server computer meets these requirements, you're good to go.

### Client Requirements

The requirements for the device that will be connecting to the server (the client) will be different depending on what device you will be using to connect to your server. 

* Android: An Android device running Android 4.1 (Jelly Bean) or newer. Newer and "flagship" devices with higher processor speeds are more likely to be able to handle Moonlight well by using the hardware video system on the device to produce smooth streaming without video stuttering or freezing. (For the geeky, if the system on a chip can decode h.264 High Profile in hardware, Moonlight will work well on the device.)

* iOS: An iProduct running iOS 8.0 or later.

* Embedded: Any embedded machine capable of compiling the source code into a working executable can run Moonlight. Embedded systems that can take advantage of their hardware video systems, like the Raspberry Pi, will run Moonnlight better.

* PC: The PC client is currently in a beta status, and can't yet take advantage of the ability to process the video using the video card's hardware, so the requirements for the PC client are currently pretty stiff. A computer of comparable power to the server is probably a good starting point.

### Internet and Network Requirements

To effectively stream from one computer to another computer or device, it's highly recommended that the server has a wired connection to your network router and that the device that will be connecting (the client) also be connected by a wired cable. 

If that's not possible, the bare minimum requirement for the server's wireless connection is a dual-band router (that broadcasts on 2.4 Gigahertz (GHz) and 5 GHz) that can handle Wireless-N (802.11n) or better. A much smoother experience will come with a wireless router and wireless card or dongle that can use the Wireless-AC (802.11ac) or newer protocol, using the 5 GHz connection.

For wireless clients, devices must be able to connect with the Wireless-N (802.11n) protocol or better, preferably in the 5 GHz band.

## 3. Installation

### For everyone

On the server, download the GeForce Experience software from http://www.geforce.com/geforce-experience/download and install it. The server may need a reboot after installation to finish setup.

Start up GeForce Experience on the server and navigate to the **Preferences** tab. Then choose the **SHIELD** option. Of the options in **Stream games from [servername] to SHIELD devices**, choose either **On my network** or **On my network and the Internet**. To set up streaming from the Internet, see the appropriate place in the Optional Cool Things section later on in the guide.

After this, follow the instructions appropriate for the platform you downloaded and installed Moonlight to. 

### Android / iOS

1. Find Moonlight game streaming in your device's app store and install it from there. Android users have the choice between Moonlight for rooted devices and Moonlight for those that aren't rooted.

If the device doesn't have access to the app store, the release packages are available from https://github.com/moonlight-stream/moonlight-android/releases (Android) or https://github.com/moonlight-stream/moonlight-ios/releases (iOS)

### Embedded

1. For embedded computers that are running Raspbian (Raspberry Pi) or Arch Linux ARM (Raspberry Pi and others), pre-built packages or an installation script are available.

	* For Raspbian and OSMC: Add a line to the file **/etc/apt/sources.list**:

		*deb http://archive.itimmer.nl/raspbian/moonlight [wheezy/jessie] main*

		Then install the package by entering the following two commands:

		*sudo apt-get update*
		*sudo apt-get install moonlight-embedded*

		Once installed, new versions will be installed during normal system upgrades.

	* For Arch Linux ARM: Use a user repository tool to install moonlight-embedded from the Arch User Repository (AUR). Afterward, new versions will be installed by running:
	
		*sudo pacman -Syu*

2. For other compatible embedded computers, Moonlight will have to be compiled from the source. Follow the directions at https://github.com/irtimmer/moonlight-embedded/wiki/Compilation

### PC

1. Download and install a Java Runtime Environment (JRE) from https://www.java.com/en/download/ (all platforms) or use the appropriate package manager for Linux distributions to install a JRE.

2. PC beta clients are available for download from https://github.com/moonlight-stream/moonlight-pc/releases - get the version that matches the architecture of the JRE downloaded (32- or 64-bit) and is for the correct operating system.

3. Start Moonlight with the command: *java -jar [name of the client downloaded].jar*

# 4. Pairing a client with a server

The first time a client connects to a server, the server needs to make sure the client knows how to communicate and is a device that the server wants to connect to. This process is called **pairing**. One server can pair to many clients and one client can pair to many servers.

To successfully pair, both client and server have to be on the same network (wired or wireless), and the server has to be running the GeForce Experience. 

### Find the server's local network address

It's helpful to know the local network address of the server, in case Moonlight has to be told where to look for your server. To find the local network address of your server, do the following:

1. Click on the Start menu and run the command prompt (cmd.exe)

2. Type *ipconfig /all* and press Enter/Return

3. A local network addresses usually takes the form of **192.168.x.yyy** - this is the information needed in case the address needs to be directly identified to Moonlight.

### Pair the client and server

1. On Moonlight for Android, iOS, or PC, once the client is connected to the network, it will scan the network for computers that have the GeForce Experience software running. If it finds one (or more), it will displpay the name of the computer it finds. Tap on the server (Android/iOS) or choose the server from the available list and click on the "Pair" button (PC) to start the pairing process.

	On Moonlight Embedded or Moonlight PC, the pairing process can be initiated from the command line using the following command:

	*moonlight -pair [the name or network IP address of the server]*

	If the server is at 192.168.0.100, the command will be: *moonlight -pair 192.168.0.100*

2. The client will display a PIN using a pop-up message. 

	On Android/iOS, the PIN disappears fairly quickly after appearing, so having something available to write the PIN down on will be handy.

3. On the server, at the same time the PIN appears on the client, a message will pop up on the server asking for the PIN displayed on the client. Enter the PIN from step 2 into the server box and click OK (or press Enter)

4. If the pairing process completes successfully, a message will appear indicating success. Once paired, a client and server do not need to pair again.

	If the pairing process was not successful, a message will appear indicating failure. If the pairing process fails, start back at step 1 and try again, generating a new PIN to enter.

5. If there are other clients to pair, return to step 1 with the next client and repeat the pairing process.

# 5. Streaming

## Starting Moonlight 

Once successfully paired, the client and server are ready to begin streaming.

### Android / iOS

Open the Moonlight app and select the server to stream from. The server will display any games or applications that GameStream has found or been told to find. Choose the game or application from the list and Moonlight will connect to the server and begin streaming.

### PC

After starting Moonlight and selecting the server from the dropdown list, click on "App List" to see a list of possible games and applications to stream.

Moonlight can also directly start Steam using the command: *java -jar moonlight-[name of client].jar -host [name or local network address of the server]*

### Embedded

Moonlight Embedded will default to launching Steam in Big Picture Mode if not specifically told to launch another game or app. To launch Steam, enter the following command: 

*moonlight stream [name or local network address of the server]*

To launch another application: 

*moonlight stream -app [name of application] [name or local network address of the server]*

## Controls

All versions of Moonlight will use any input devices attached to the client to control the application launched from the server. Keyboards, mice, game controllers, whether wired or wirelessly, can be used, assuming they have been set up correctly on the client. This may require the use of other apps, drivers, or button mapping files to ensure that the input devices work correctly. Devices that have been set up for use on the server may also be usable, but they may be given a lower priority or used as controls for a second or higher-numbered player in various games. There is a workaround for this. By renaming **rxinput.dll** in **C:\Program Files\NVIDIA Corporation\NvStreamSrv** (and in **C:\Program Files (x86)\NVIDIA Corporation\NvStreamSrv** on 64-bit Windows), the server will stop accepting control input from the client and only use controllers or peripherals connected to the server. This workaround will have to be re-done every time GeForce Experience updates.

### Android/iOS

Moonlight for Android and iOS use the touch screen as a way of controlling the mouse cursor. Multi-touch devices can emulate more mouse functions than single-touch devices.

* Swiping across the screen moves the mouse cursor in the direction of the swipe.
* Tap once with one finger to left-click.
* Tap and hold in the same place to start a click and drag. After a short while, swipe the finger to drag in the direction of the swipe.
* Tap with two fingers to right-click. 
	* A reasonably consistent way of getting a right-click is to tap and hold with one finger and then tap with the second finger before releasing both fingers. The timing takes a little practice, but the results are pretty consistent. 
* Tap with three fingers to open the on-screen keyboard. Only some keyboards work with Moonlight for Android - the Hacker's Keyboard (https://play.google.com/store/apps/details?id=org.pocketworkstation.pckeyboard) seems to work well for everything but the arrow keys.

# 6. Optional Cool Things

## Stream over the Internet

By default, GeForce Experience and GameStream will only stream over your local network. To stream over the Internet, specific ports must be opened to allow communication between computers, and Moonlight will have to be explicitly told what IP address to connect to, which will be a different address than one on your network. 

1. On the router controlling the network that the server connects to, in the port forwarding section, open the following ports on the following protocols:
* TCP:
	* 35043
	* 47984
	* 47989
	* 47995
	* 47996
	* 48010
* UDP:
	* 47998
	* 47999
	* 48000

2. To find the external IP address of your server, when connected to your network, use a service like http://www.whatismyip.com to determine the IP address another computer uses to talk to you.

	* **Note:** Some Internet Service providers change the external IP address in use by any given subscriber on a regular basis. Since Moonlight needs to connect to the right IP address, this change can cause problems for Moonlight. Using a dynamic DNS service like No-IP (http://www.noip.com) will give Moonlight a consistent name to use for connecting, even if the IP address that's associated with that name changes a lot. 

3. Type the external IP address or name into the IP bar (PC), command line (PC / Embedded) or, on Android or iOS, tap on the plus key when you see all the possible servers to connect to, and a dialog will pop up to enter in an IP address or name, and then connect as normal to your server. Enjoy streaming over the Internet!

## Stream other applications and games

Moonlight and GeForce Experience will regularly scan any directories you choose for games that it knows how to handle, but not every game owned will appear in the listing, so sometimes games will have to be added manually. Additionally, other non-game applications can be streamed using GameStream through Moonlight. To add custom games or applications to Moonlight:

1. Start up GeForce Experience on the server and navigate to the **Preferences** tab. Then choose the **SHIELD** option.

2. Click on the plus sign (+)

3. Navigate to the executable file (on Windows, this will almost always be a file that ends .exe if the file extensions are visible), click on it, and choose "Open".

4. Give the application a name to remember, and optionally, choose an icon to represent the program.

5. The next time Moonlight opens and displays the App List (or the -list option is used on Moonlight Embedded), the newly added programs and games should be displayed and ready to stream.

6. If quitting an application doesn't stop Moonlight, press *Ctrl+Shift+Alt+Q* on Moonlight Embedded or Moonlight PC to quit the streaming session. On Moonlight Android and iOS, pressing the home key will switch out of the streaming session and allow selection of the **Quit Session** option from the Application List when returning to Moonlight. 

### Stream the Windows Desktop

In addition to specific applications and games, the Windows desktop of the server can be streamed through Moonlight, making Moonlight an effective and free remote desktop application as well as a game streaming application. To get the Windows Desktop on Moonlight: 

1. Start up GeForce Experience on the server and navigate to the **Preferences** tab. Then choose the **SHIELD** option.

2. Click on the plus sign (+)

3. Navigate to **C:\Windows\system32** and click on **mstsc.exe** (the .exe may not be visible, depending on your preferences)  and choose "Open".

4. Give the new application a name to remember (Windows Desktop), and optionally, choose an icon to represent the program.

5. The next time Moonlight opens and displays the App List (or the -list option is used on Moonlight Embedded), the name you gave the Windows Desktop program should be available to choose.   

6. To quit from the Windows Desktop, press *Ctrl+Shift+Alt+Q*

## Fine-tune streaming options

Moonlight will default to a certain size and quality of streaming, depending on the client in use. If these defaults don't work, or the client, server, and network can handle a more robust set of streaming options, Moonlight can be configured to stream in different ways.

On Android/iOS, these streaming options can be accessed by tapping on the gears icon on the screen that shows all the possible servers to connect to. On PC and Embedded, these options can be called using the command line. 

Some of the common options are:

* -fs : launch in full screen
* -720 : use 1280x720 resolution (default)
* -1080 : use 1920x1080 resolution
* -30fps : use 30 fps stream (default)
* -60fps : use 60 fps stream
* -bitrate : change the bitrate (in Kbps) that Moonlight aims for with streaming. Lower values may result in smoother streaming at the cost of video quality. 

# 7. Troubleshooting

* Many issues with connection, pairing, and streaming can be fixed by rebooting the server and the client. 
* After checking to see that the GeForce Experience software is running, try lowering the streaming options to 720 and 30fps, and lower the bitrate to see if things improve.
* If possible, make sure both client and server are either connected by wire or by a 5 GHz wireless network. 
* Some applications will crash if launched directly from Moonlight. Using Steam or another launcher may help. (http://support.steampowered.com/kb_article.php?ref=2219-YDJV-5557 has instructions on adding non-Steam applications to Steam)
* If it still doesn't work, some Android devices have a worse experience when Bluetooth is active. Turning off Bluetooth may improve video quality.
* Should everything not work, cleanly uninstall the GeForce drivers, the GeForce Experience software, reboot the computer, and then reinstall and re-set up the server and client.

# 99. Other Things

Trademarks used in this document are the respective property of their owners. No endorsement is implied or explicit from the owners of those trademarks.

Moonlight was created by <a href="http://case.edu/">Case Western Reserve University</a> students as a project at the <a href="http://mhacks.org/">MHacks</a> hackathon in 2013 and further developed at MHacks and <a href="http://hackcwru.com/">HackCWRU</a> in 2014.

Moonlight Embedded is an unofficial fork of Moonlight and the product of irtimmer (https://github.com/irtimmer/)

Information about Moonlight can be obtained by e-mailing info@moonlight-stream.com or by reading and visiting <a href="http://forum.xda-developers.com/showthread.php?t=2505510"> the Moonlight XDA Developers Thread</a>.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Moonlight User Guide</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/HeofHIShirts/moonlight-user-guide" property="cc:attributionName" rel="cc:attributionURL">HeofHIShirts </a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

What this means is that if you use this document to make your own document, you must credit HeofHIShirts (https://github.com/HeofHIShirts or https://neocities.org/HeofHIShirts) and then release your own document under the same or a similar license to this one.

This document can use your help! Updates, more information, and error corrections are entirely welcome, and I hope this will be a great companion to help others use Moonlight. Thank you!