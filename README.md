# TomTom Sports Connect(Ubuntu 20.04/Mint 20)<br />

Guide to install TomTom Sports Connect on 64-bit Ubuntu 20.04 or Mint 20.<br />

![](tomtom-sports-connect.png)

Edit this file `/etc/apt/sources.list` and add this line to the end of it.

`deb http://security.ubuntu.com/ubuntu bionic-security main`

Install required packages:<br />
`sudo apt update && apt-cache policy libssl1.0-dev`<br />
`sudo apt install wget libssl1.0-dev libgl1-mesa-glx`

Download tomtom app and dependencies:<br />
`wget https://sports.tomtom-static.com/downloads/desktop/mysportsconnect/latest/tomtomsportsconnect.x86_64.deb`<br />
`wget http://archive.ubuntu.com/ubuntu/pool/universe/g/gstreamer0.10/libgstreamer0.10-0_0.10.36-1.5ubuntu1_amd64.deb`<br />
`wget http://archive.ubuntu.com/ubuntu/pool/universe/g/gst-plugins-base0.10/libgstreamer-plugins-base0.10-0_0.10.36-2ubuntu0.2_amd64.deb`<br />

And install them:<br />
`dpkg -i libgstreamer0.10-0_0.10.36-1.5ubuntu1_amd64.deb`<br />
`dpkg -i libgstreamer-plugins-base0.10-0_0.10.36-2ubuntu0.2_amd64.deb`<br />
`dpkg -i tomtomsportsconnect.x86_64.deb`<br />

You can run tomtom from start menu or terminal (for logs) with:<br />
`/usr/local/TomTomSportsConnect/bin/TomTomSportsConnect`<br />

It didn't work when I ran it as regular user and I got "We could not connect to your watch", so I needed to run it as root with sudo.

You can edit launcher to make it execute as root.<br />
Open `/usr/share/applications/tomtomsportsconnect.desktop` (as root) in any editor and set following value for Exec<br />
`sh -c "pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY /usr/local/TomTomSportsConnect/bin/TomTomSportsConnect"`

Download and set pkexec policy for tomtom application:<br /> 
`wget https://raw.githubusercontent.com/cromat/TomTom-Sports-Connect-Ubuntu-20.04-Mint-20-/main/org.freedesktop.policykit.tomtomsportsconnect.policy -P /usr/share/polkit-1/actions/`
`sudo chown root /usr/share/polkit-1/actions/org.freedesktop.policykit.tomtomsportsconnect.policy`
