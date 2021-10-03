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
