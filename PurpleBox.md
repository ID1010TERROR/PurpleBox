# Purplebox Overview
A Purplebox setup takes the concept of "hacklabs" to the next level by combining it with the SecurityOnion NSM (Network Security Monitor) which provides you greater visibility into your attacks and the effects they have on the wire. PurpleBox gets its name from the concept of a "Purple Team", being the observer/unifier between BlueTeam and RedTeam operations that provide a proper narrative of the events that took place.

This setup will assist you in properly recording that narrative as systems are attacked and also fascilitate analysis of the systems for forensic artifacts. This setup can be used as a training aid or just a great way to complete various PCAP centric CTFs/forensics challenges available online. Not only can you use this for monitoring in real time, but it is trivial to play back old PCAP data using tcpreplay and get the same effect. 

The setup fascilitates greater insight to both Offensive and Defensive Cyber Operations by allowing post engagement analysis that highlights exactly what happened on the wire. On the one hand it allows BlueTeam to hunt for and develope new indicators of compromise, while also allowing RedTeam to visualize how its attacks could be detected by BlueTeam and provides deeper understanding of various attack methodologies. Basically, if you want an FOSS hacklab that goes beyond simple virtualizing boot-to-roots and helps you truly understand what's going on behind the scenes, then this is the kind of setup you want.

# Basic Setup
1. **Virtualbox** - This tutorial will use Virtualbox, but the same setup could easily be repeated across any modern hypervisor. This tutorial assumes you are able to locate and install that software on you own. 

2. **Security Onion** - At its core a Purplebox utilizes the SecurityOnion NSM (Network Security Monitor) created by Doug Burks at Security Onion Solutions, which itself combines many of the giants in the opensource network security monitoring and analysis realm such as: Bro, Snort, Surricata, Wireshark, ELSA, Netminer, Sguil, Xplico, Squert, and many more into one easy to setup system that can record and analyse network traffic. 

> You can locate the ISO for SecurityOnion at their [Github Account](https://github.com/Security-Onion-Solutions/security-onion/blob/master/Verify_ISO.md), download the ISO and follow the instructions on the download page to ensure you have a valid copy of SecurityOnion. A very thorough walkthrough for installing SecurityOnion on Virtualbox is located on their [Github Wiki](https://github.com/Security-Onion-Solutions/security-onion/wiki/IntroductionWalkthrough). 
>
> The only place you will deviate from this Walk Through is when you get to your network interface setup in virtualbox settings. You will set your first adapter (your management interface) to "Bridged" (this basically treats the system as if it were another computer connecting to your wireless router) and the second adapter to "Host-Only Adapter" instead of "Internal". This is the adapter that will be used for sniffing traffic, and since the idea is that you may also be running boxes that are insecure by design (ie. Metasploitable), we need to ensure we are limiting the range our virtual environments have, especially if we are connected to the internet. Also for the sake of simplicity, running the system in evaluation mode should work fine for our purposes.

3. **Attack System** - After you've completed the setup of your NSM you can go ahead and install your attack machine, for this tutorial we'll be utilizing [Kali](https://www.kali.org/). Regardless of which systems you choose just remember to also give it Network Adapters configured for "Host-Only" otherwise they won't be able to connect to the "Host-Only" network your vulnerable box SHOULD be on. You may opt to add an additional "Bridged" adapter to your attack machine, doing so will allow you to reach the internet and install additional software. However bear in mind, if you do this you will likely need to create a new interface entry in the bottom of your /etc/network/interfaces file such as:

~~~~
auto eth1
iface eth1 inet dhcp 
~~~~

After doing this be sure to run:

~~~~
sudo ifup eth1
~~~~

and your new interface should pull an IP for your routers DHCP pool, be sure to confirm by checking ifconfig.


3. **Vulnerable System** - Next, you will install your Vulnerable System, there are many great boot-to-roots available for practice on [Vulnhub](http://www.vulnhub.com), for this tutorial we'll be using [Metasploitable2](https://www.vulnhub.com/entry/metasploitable-2,29/). Regardless of which systems you choose just remember to also give it Network Adapters configured for "Host-Only" again this is because you are placing a purposefully vulnerable system on your network, and want to limit it's exposure as much as possible.

4. **Verify Connectivity** - After you've done so, verify connectivity by ensuring each system can be reached by the other via ping request. Then perform one final test by running a full Nmap -A scan on your vulnerable system from your attack system, if all goes right you'll see sguil (in Security Onion) light up like a christmas tree with all of the alerts it receives. 

# Walkthrough
Now that you have your system setup, lets go through some basic network analysis with SecurityOnion as our surveillance system. We'll start where all good attacks start. 

## The Recon
Now from a BlueTeam perspective obviously your enemy has already done their passive recon, whois lookups, internet archives, basic OSINT research. We won't be able to detect much of that but as soon as their recon turns from passive to active network recon, we'll get our earliest indicators that someone is up to no good, and obviously the earlier we can detect them within the [Cyber Killchain](http://www.lockheedmartin.com/content/dam/lockheed/data/corporate/documents/LM-White-Paper-Intel-Driven-Defense.pdf) the better positioned we will be, to prevent them from doing further damage to our network... 

<p style="text-align: center;font-weight:bold"> To be continued.<p>




# References

- https://www.virtualbox.org/manual/
- https://github.com/Security-Onion-Solutions/security-onion/wiki
- https://groups.google.com/forum/#!forum/security-onion
- http://www.lockheedmartin.com/content/dam/lockheed/data/corporate/documents/LM-White-Paper-Intel-Driven-Defense.pdf
