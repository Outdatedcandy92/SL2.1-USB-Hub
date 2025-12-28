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