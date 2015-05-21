# Modifications (compared to authentic Freakduino) #

## DC-DC Voltage Up Converter ##

Originally, I couldn't find the TO-98 (through-hole) packaged Holtek HT7750A, at all. So I researched and found part of similar function, the Texas Instruments TPS61222, in it's tiny SC-70 SMD package.

Later, I found and acquired the Holtek part from a Chinese supplier. But I decided to stick with the SMD part anyway, because I simply prefer SMD to through-hole components, these days.


## Digital Level Shifter — GTL2003 instead of FXMA108 ##

Again, I originally could not find a supplier for the FXMA108 and again, finally found and acquired the part from China. But the GTL2003 is an easer part to handle by hand and I'd already done the routing design by then. So I'm sticking with that, too.

Note that this part's equivalent /ENABLE pin has reverse sense, to the FXMA108. The the circuit around JP2 was modified accordingly.

## FT232RL USB-to-Serial Converter ##

The option exists to go open hardware for this part, by changing to the ATmega16U2, with a 16MHz xtal and firmware from the Arduino archives. I think it would be a very tight squeeze to get the AT'16U2 on the board, mostly due to the need for ISP programming pads. But it does look doable, maybe.

(Incidentally, the power consumption of the ATmega16U2 at 16MHz/5V and FT232RL are both about the same. But it matters not anyway, because that circuit is only powered up when a USB cable is connected.)



## UNO `R3` Additional SDA/SCL pins (D14/15) ##

I briefly considered adding the extra Arduino pins, beside D13, for I2C SDA and SCL. But since these already appear on the, "analog in" pins 4 an 5, I see no point in doing so. Instead, I have simply added silk text SDA and SCL next to analog pins 4 and 5. ([r79](https://code.google.com/p/kicad-freakduino/source/detail?r=79))

## Custom Routing and Lots of Learning around the RF Section ##

I never bothered looking for the original author's CAD files for the PCB, because I wanted to gain my own experience in routing up a board of this nature -- especially regards the 2.4GHz RF section.

RF circuitry can be like black magic. It's just not as simple as connecting two or more points together with coper and calling it a job done well. PCB track widths, lengths, spacing from each other and to ground planes and even the thickness and precise constituency of the PCB board itself, all become important at these high frequencies!

As it happened, I did make a number of newbie/amateur mistakes in just those regards, realising errors only after days of studying and reflection, having initially thought I'd got it right -- but far from it. After reading the data sheets and reviewing knowledge from over the years, I think I finally arrived at an appropriate layout.

I also took a magnifying lens to the physical Freakduino boards I had purchased, to see how Akiba had done things in the RF section. Initially, I didn't understand why some of the things were done in such a way. Moreover, I didn't even notice some details -- for days -- which in fact turned out to be quite important.

I wanted to make sure I could state confidently _why_ each and every little thing was the way it was in the Freakduino design. I didn't want to assume that it was all done right, either. Reading data sheets and refreshing my matched line theory for 2.4GHz got me there eventually -- I hope. It also appears that Akiba did a fine job, indicating that he has at least as good a handle on the subject as I have managed to cobble together, which is good to know.

In any case, the RF section is done as best I can calculate or theorise it can be, using my available skills and current knowledge. Eventually, I ended up with nearly the same layout as Akiba, for presumably the same technical reasons. Truly, that took several iterations and a lot of reading to actually arrive at. So, I really found it all to be an interesting and valuable exercise.

I do still wonder if there shouldn't ideally be an additional ferrite bead/choke, separating (RF wise) digital and analog grounds, at the digital Vcc corner of the RF chio's grounding pad. I kind of accidentally made provision for adding a ferrite, by cutting just one relatively narrow track. But didn't actually install pads for one. Perhaps I should have.  This leads me onto the next, related topic ...

What I don't know, is how to really test this thing's performance. I have a frequency counter theoretically cable of clocking a 2.4GHz signal at 8 digits resolution, to see if I'm at least on channel. (Slim chance it won't be anyhow.) But I have no idea how to go about testing tuned circuitry attenuation from transmission line impedance mismatch etc, at this ultra-high frequency (UHF). I imagine there is a test procedure published somewhere, probably involving an output power calibrated signal source with high quality 50-ohm termination, to test the receiver performance again factory specifications.  Likely the same for power output at the SMA antenna socket. Knowing spectral purity of a steady carrier and being able to test that under various digital noise conditions would be nice, too. But I simply don't have access to any equipment of that nature -- certainly not any that would work at these high frequencies.

So I'm just going to have to trust in the theory and my application thereof and hope I've got things good enough. That said, I am pretty confident, given the research and care I eventually put into the design and that I believe I understand precisely why each little detail is needed. If I'm unlucky and it turns out that I get really lousy range out of my design, then I'll be stuck for a solution, for sure. I don't like that prospect, at all.  If all goes well, I can see a number of matchbox sized wireless sensors or controllers springing up around my home -- all hand built. That should be fun!