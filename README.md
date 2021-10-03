## Intro

It's a guide on using a Raspberry Pi as a Wi-Fi access point to connect BMW cars wirelessly to phones and laptops, e.g., to use `BootMod 3`, `xHP`, `xDelete`, etc.

This DIY guide makes sense if you **already** have an idle Raspberry Pi or you're a geek like me and want to know how it works by getting your hands dirty. Otherwise, I would recommend going with one of these devices:

|                                                                                              Device                                                                                               |                                                                                                                           Comment                                                                                                                            |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| <img src="images/bootmod-3-wi-fi-adapter.webp" alt="BootMod 3 Wi-Fi adapter" width="200" /> BootMod 3 Wi-Fi adapter <br> from [protuningfreaks.com](https://protuningfreaks.com) <br> for $149.00 | It's a Raspberry Pi 3 configured the same way as described in this guide; you end up with two cables: an ENET cable (purchased separately) to connect the adapter to a car via an OBD2 socket and another one to connect the adapter to the source of power. |
|                        <img src="images/enet-wi-fi-adapter.webp" alt="ENET Wi-Fi adapter" width="200" /> ENET Wi-Fi adapter <br> from [eBay](https://ebay.com) for $90.00                         |                             True wireless - plug and play as sellers say. I haven't tested it yet if it's so sweet. Maybe one day I am fed up with wires in my car, I will grab one to test and update this guide with a review.                             |

## Prerequisites

- Raspberry Pi with an Ethernet port and a Wi-Fi module + microSD card.

  _I am using a Pi 4 Model B with 4GB of RAM and SanDisk Edge A1 U1 Class 10 32GB microSD card._

- Computer running macOS/Windows/Ubuntu to install Raspberry Pi OS to a microSD card.

  _You are lucky if your computer has an onboard microSD card reader; otherwise, you need an adapter._

- Cable that is good enough to deliver power to your Raspberry Pi.

  _If the cable can't deliver enough power, then the CPU clock speed will be limited. But it shouldn't be a problem since we won't run any compute-intensive tasks._

- BMW ENET cable (OBD to Ethernet) to connect a car to your Raspberry Pi.

- LAN cable to connect a Raspberry Pi to a router.

- **(Optional)** Power bank that is good enough to power up your Raspberry Pi.

  _Google can help with the choice. It's optional since you can use a Type-A or Type-C socket of a car; I've seen some guys on forums doing it way, but I prefer an independent power supply._

- **(Optional)** HDMI to micro-HDMI cable for debugging purpose.

- **(Optional)** Raspberry Pi case and fan.

  _It's optional since it's purely for your convenience. In the case of Pi 4, I would go with official ones, especially considering that official ones cost the same or even less than custom ones._

## 1. Install Raspberry Pi OS to a microSD card

Download Raspberry Pi Imager from [raspberrypi.org](https://www.raspberrypi.org/software/), install it on your computer, and run.

Choose `Raspberry Pi OS Lite` for `Operating System` and your microSD card for `Storage`.

Press `CTRL + SHIFT + X` to show `Advanced options`.

- Enable SSH and select an authentication method.

  _If you don't know how to use public-key authentication, go with a password._

- Configure Wi-Fi and locale settings.

  _**WARNING!** Not all Raspberry Pi's (e.g., Pi 3 Model B) support 5 GHz band._

Click on `Write` and wait for the flashing process to finish.

## 2. The first Raspberry Pi launch

Insert a microSD card into a powered-off Raspberry Pi.

If you have an HDMI to micro-HDMI cable, connect your Raspberry Pi to a display to read the logs - it will help debug if you face some issues.

Power up a Raspberry Pi and wait. The first launch is always more extended (~1.5 minutes in my case) than subsequent ones (~30 seconds in my case) due to a microSD repartitioning and multiple reboots.

## 3. Connecting to a Raspberry Pi

On Linux or macOS, connect to a running Pi via SSH client with a command:

```sh
ssh pi@raspberrypi.local
```

On Windows, you have at least two options:

1. Download, install and use [PuTTY](https://www.putty.org/) client

2. Install [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu) (Linux based OS) on [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) and use its command line

You can face an issue with resolving mDNS here if you are using an out-of-date Windows 10. You can try to update it, but the quick-and-easy solution is to use a Pi's IP address instead of `raspberrypi.local`. There are at least two ways where you can find it:

1. Connect to a router admin panel and look for a list of all the connected devices.

   _In the case of a router for geeks (e.g., MikroTik) look for a DHCP server and leases._

2. Connect a Pi to a display, and at the end of the logs you will find:

   ```
   My IP adress is XXX.XXX.XXX.XXX
   ```

I prefer using public-key authentication not to enter the password all the time, especially when a password is long and/or contains special symbols. Also, I don't particularly appreciate reusing SSH keys, so I have a standalone SSH key to log in to a Pi and for nothing else. Such an approach requires some changes to `~/.ssh/config`:

```
...

Host raspberrypi.local
    IdentityFile ~/.ssh/raspberry-pi-4
```
