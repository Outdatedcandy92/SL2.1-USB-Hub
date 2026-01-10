# USB Hub

## 27/12/25

I was pretty bored and ran out of ideas today so I decided to speedrun a USB Hub; to be honest I have been in need of a usb hub for a LONG time but always procrastinated making one (since onboard btw).

I decided to use the SL2.1S chip because it's a fairly easy IC to use; requires no external crystals and have 4 downstream facing ports which is good enough for me (though I did spent a lot of time looking at alternatives from microchip and ti but they were too overkill for what I needed). 
I had to first translate the whole datasheet because it was originally in Chinese; the datasheet says that it does require and external crystal to work but I referred to some designs online and they seem to be working fine without one, so I went ahead with my schematics and connected xin to gnd.
![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/1701ba982bf69fce_FZaBAAAAAAA7LGhTm50kqzotD0AAAAAALA7TEsFAAAAAAD0FckNAAAAAACgr0huAAAAAAAAfUVyAwAAAAAA6CuSGwAAAAAAQF_R3AAAAAAAAPqK5AYAAAAAANBXJDcAAAAAAIC_IrkBAAAAAAD0FckNAAAAAACgr0huAAAAAAAAfUVyAwAAAAAA6CuSGwAAAAAAQF_R3AAAAAAAAPqK5AYAAAAAANBXJDcAAAAAAIC_IrkBAAAAAAD0FckNAAAAAACgr0huAAAAAAAAfUVyAwAAAAAA6CuSGwAAAAAAQF_R3AAAAAAAAPqK5AYAAAAAANBXJDcAAAAAAIC_8v8Hq3tav2whEE0AAAAASUVORK5CYII_)

I added a 100nf and 1uF capacitor for each power pin (although this was probably not required); after this I went ahead with my PCB design (the fun part!!); started off by assigning net classes and color coding them to give me a better view as usual.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/67a8138681e5c95c_AZpmmkKR5xsWAAAAAElFTkSuQmCC)

Layout was pretty easy as this PCB hardly had any components; I went with a 50x20mm board to keep the hub as tiny as possible. Here are some pictures of the routing process

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/9c25f802776cb63c_D7IRugqkG_gwAAAAAElFTkSuQmCC)

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/6a3449e33542c962_8PBG6iRAeGznUAAAAASUVORK5CYII_)

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/e1b7bf12958ec086_4fIM4UaOQzkNkAAAAASUVORK5CYII_)

^This was the finished board, I went with 2 layers and routed all the data and cc traces on top, poured ground on bottom and routed power; I did make sure to not have any splits in the ground plane under the data pairs!

And another thing I added was a power indicator led; its just a green led connected to the vbus to indicate power detection. For this I added two 5.1k resistors in series to limit current which adds up to 10.2k ohm in series with the LED. Now you may think that this is way to much and that the led would barely glow, but you'd be wrong; 0402 LEDs are super efficient and super bright, even at 10K resistor in series at 5v the LED is bright enough to be seen in a lit room.
Oh and yeah the reason I went with two 5.1k resistors in series instead of just one 10k resistor was to optimize the BOM; even though the project is pretty cheap, why use more components than needed right.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/9298f5f434e463b8_D2tOAfkqJWx3AAAAAElFTkSuQmCC)

After this I spent a couple of minutes adding some basic silkscreen and assigning lcsc parts; generating the BOM with prices and finally setting up a github repository.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/99caca37fdb5b144_IsbxN0gAAAABJRU5ErkJggg__)


Anywho this is how the final board looks like!

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/38b9c80d7173a56a_wHSOUtkZKaSUQAAAABJRU5ErkJggg__)


## Time Spent: 3.5 Hours

---

## 9/01/26

Decided to add some more features to the USB hub. I figured why not add an onboard USB to UART chip so I can just use the hub as a debugging tool, and so I began my research and found the MCP2221A.

The MCP2221A is a small USB 2.0 to I2C/UART convertor chip by microchip which came in a small 4x4 QFN package.
![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/5699007e69e34220_sKe7EEIIIYQQQgghhBBCCHGwktBdCCGEEEIIIYQQQgghhGgkEroLIYQQQgghhBBCCCGEEI1EQnchhBBCCCGEEEIIIYQQopFI6C6EEEIIIYQQQgghhBBCNBIJ3YUQQgghhBBCCCGEEEKIRiKhuxBCCCGEEEIIIYQQQgjRSP4fEZ0wpNXhGUgAAAAASUVORK5CYII_)


I also decided to add another SL2.1S IC and daisy chain it with the first one to get a total of 7 downstream USB ports, out of those 7 downstream ports I used 6 for USB and 1 for the MCP2221.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/8f9b167a13664b9d_yfQMaBWnySifQAAAABJRU5ErkJggg__)


Wiring up the MCP2221 was pretty straightforward, the datasheet was also helpful and I found that the 4 GPIO pins have a default function as indication for activity and so I wired those up to some LEDs.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/7199c8bb0bb6842a_jiOtfQAAAABJRU5ErkJggg__)


Now the UART/I2C indicators go low when they sense activity, but the USB_CFG goes high/low depending on if the USB is successfully configured or in suspend mode.

Moving onto the PCB, it was pretty clear to me that I'd have to start over again, and so I deleted everything I originally had and started fresh with a new layout.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/3f8c511bd03c0ad5_Ee3TldjSpwLB8SZxI4VCoVAo4wWHLDoKhUKhUMYKVOgoFAqFMq6hQkehUCiUcQ0VOgqFQqGMa6jQUSgUCmVcQ4WOQqFQKOMaKnQUCoVCGddQoaNQKBTKuIYKHYVCoVDGNVToKBQKhTKuoUJHoVAolHENFToKhUKhjGuo0FEoFAplXEOFjkKhUCjjGip0FAqFQhnXUKGjUCgUyriGCh2FQqFQxjVU6CgUCoUyrqFCR6FQKJRxzf8HRVSMoRTRydwAAAAASUVORK5CYII_)

I went with a symmetric layout (kinda) with 4 USB-A ports on one side and 4 USB-C ports on the other side.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/b118b77cbddba4db_O3YsAAAAADDI33oU_wojAACYyXgAAAAAAJjJeAAAAAAAmMl4AAAAAACYyXgAAAAAAJjJeAAAAAAAmMl4AAAAAACYyXgAAAAAAJjJeAAAAAAAmMl4AAAAAACYyXgAAAAAAJjJeAAAAAAAmMl4AAAAAACYBfI5YjB6iDxZAAAAAElFTkSuQmCC)

After that I just routed everything and fixed the pinouts in the schematics based on which port was the closest, and in the end I ended up with this.

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/47413792aa328678_wMdIGHDNaJjtgAAAABJRU5ErkJggg__)

![image](https://hc-cdn.hel1.your-objectstorage.com/s/v3/2933ab49c4cf07fa_IiIiIiKiPMDwR0RERERElAf0F1989YPahURERERERDS9sPJHRERERESUBxj_iIiIiIiI8gDDHxERERERUR5g_CMiIiIiIsoDDH9ERERERER5gOGPiIiIiIgoDzD8ERERERER5QGGPyIiIiIiojzA8EdERERERJQHGP6IiIiIiIjywP8HZ44BE0sVroQAAAAASUVORK5CYII_)


Also decided to add mounting holes on the PCB as you can see, decided I might need them in the future if I plan on making a case. 
Also spent a few minutes just updating the BOM and getting prices from lcsc and JLC.

## Time Spent: 3 Hours

