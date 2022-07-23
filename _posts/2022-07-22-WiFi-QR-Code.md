---
layout: post
date: 2022-07-22
author: Jason Brown
title: Wi-Fi QR Code via Linux CLI

---
A few days ago, this blog post on joining [guest Wi-Fi using a QR code](https://blog.jgc.org/2022/07/guest-wifi-using-qr-code.html) came across my RSS feeds. It's something I've been meaning to get around to for a while, since I have an obnoxiously long password and my wife and guests are often frustrated by it. What usually happens is that they try to type it a time or two, miss a character somewhere, and then get frustrated and ask me to type it for them. It was high time for me to upgrade our little Wi-Fi password sign.

Initially I was just going to look for a QR code generator and plug in the Wi-Fi info string, print it out, and call it good. As was mentioned in the linked blog post, all those Wi-Fi QR codes contain is a string formatted like this:

`WIFI:S:<Network SSID>;T:<WPA|WEP|blank>;P:<Network Passkey>;H:<Hidden? true|false>;;`

So it would be simple to just replace the relevant bits of the string with my network details and be on my way. I went to go search for a qr code generator online, but for some reason decided to make my search query a little more specific than was necessary, something like "wifi qr code generator." I spotted this neat little project, [wifi-card](https://github.com/bndw/wifi-card) that you can try out at [wificard.io](https://wificard.io/). It's a web interface that has input fields for the SSID and password that generates a handy little card for you to print out. This was more than I needed though as we already had a sign and I just wanted the QR code. (Yes, I know I could have just taken the QR code from this.)

Next, I decided to search the Artix software repositories for a simple offline QR code generator. I found the popular [qrencode](https://fukuchi.org/works/qrencode/) library and utility which would work great for my purposes. Now qrencode can generate you a nice little .png of your encoded data, but it also has a neat feature where you can output your QR code to the terminal as ASCII or UTF-8 block characters!

`qrencode -t utf8 "WIFI:S:SSID;T:WPA;P:Password;H:false;;"`

prints out:

```
█████████████████████████████████████
█████████████████████████████████████
████ ▄▄▄▄▄ █ ▀▀▄  ▄ █▄▀ ██ ▄▄▄▄▄ ████
████ █   █ ███ ▄▄█▄▀██▀▄▀█ █   █ ████
████ █▄▄▄█ █ ▄▄ █▄▄ █ █ ██ █▄▄▄█ ████
████▄▄▄▄▄▄▄█ █ ▀ █▄▀ ▀ █ █▄▄▄▄▄▄▄████
████   █▀ ▄▀   ██ ▄█ ▄▀▄▀ ▄▄ ▀█  ████
████▄▀▀█▀ ▄▄▄▀█▄█▀█▄█ █▄▄▀▄ ▀▄█▀▀████
████▄▄  █ ▄█▀ █▄ ▄██▀▄ ▄█▀█▄▄▀▀▄▀████
████▀██▄▄▄▄▀▄██▀ ▄ █ ▄ ▄ █▄▀▄ ▀▀▄████
██████▀ ▄▄▄█ ▀▄██  ██ ▄▄█ ▄▀  ▄█ ████
████▄▄██  ▄▀▀ █▄█▀█ █▀█▀ ▄▄ ▀    ████
████▄▄▄███▄█▀▀█▄ ▄██▀▄▀█ ▄▄▄ ▀▀ █████
████ ▄▄▄▄▄ █▀▀▄▀ ▄ ▄▄█▄▄ █▄█ ▄█▀█████
████ █   █ ███ ██  ██ ▄▄▄ ▄▄▄▀██▄████
████ █▄▄▄█ █  ▀▄█▀███▀█▀▄    █▄▄ ████
████▄▄▄▄▄▄▄█▄▄▄▄▄▄███▄▄██▄██▄▄▄▄▄████
█████████████████████████████████████
█████████████████████████████████████
```

*Note, this may or may not actually scan for you depending on how your browser renders it. Font matters. See aspect ratio notes below.*

Neat! All I have to do with that is send it directly to my printer, cut it out, and tape it to the sign. To do that:

`qrencode -t utf8i "WIFI:S:SSID;T:WPA;P:Password;H:false;;" | lp -d <printer>`

Note that I change the format from utf8 to utf8i which inverts the colors so that it looks nicer on a white background. It prints out, and looks okay, though the aspect ratio is a bit off. I test it using my phone and it works perfectly. I'm connected in seconds.

## QR Code Aspect Ratios
This is where you have to be careful. That square aspect ratio is integral to the QR codes functionality. I noticed that one of the prints I made while experimenting with different settings came out a bit wider and shorter than the others and I had a difficult time getting it to scan. The biggest factor to making this work is ensuring it prints with a monospaced font so that it comes out square.

This got me wondering, how far off of square can a QR code be before it stops working? QR codes are generally pretty fault-tolerant as they have some neat built in error correction, so I did a bit of testing to find out.

First, I generated a test qr code image.

`qrencode -t png test.png test`

![test.png](/assets/images/2022-07-22-test.png)

Then I used ImageMagick to scale it up:

`convert test.png -resize 1000x1000 test.png`

And then resized the image over and over until I could no longer scan the code reliably.

`convert test.png -resize 100%x60% widened.png; convert test.png -resize 70%x100% narrowed.png`

![widened.png](/assets/images/2022-07-22-widened.png)
![narrowed.png](/assets/images/2022-07-22-narrowed.png)

And those are the thresholds I found, at least with my particular phone and QR scanner app. Optimal is of course 1:1, widest seems to be 5:3, and narrowest seems to be about 7:10. I was not able to get anything beyond those cutoffs to scan, and right at the border it sometimes took a dozen or more seconds of moving the camera around to get it to scan. The thresholds actually seem to be pretty rigid, I was able to get 72%x100% to scan reliably but shaving off another two percent made it very difficult to scan, and three percent made it impossible. Curious that it seems to be more resistant to changes in the height than the width.

## Conclusion
I've now got myself a nice little Wi-Fi QR code that will hopefully save me from dealing with frustrated guests! I also added a new little utility, qrencode, to my CLI toolbox. Not a bad little diversion for a Friday afternoon.
