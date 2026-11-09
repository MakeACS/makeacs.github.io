---
icon: lucide/circle-dollar-sign
---

# 4. System Price

One of the main development goals of MakeACS was to create a system that did not cost much to implement nor maintain. Below is a breakdown of the costs of implementing MakeACS;

!!! note
    All prices listed are for the price of materials and BOM items, and assumes you are doing any assembly/installation yourself.

## Hardware Cost

The Access Control Hardware is the most expensive part of a MakeACS deployment, an average setup comes out to around $200 per machine.

Let's look at an example; what would it take to put MakeACS on all five sewing machines in our textiles shop? Sewing machines plug directly into the wall, so simply putting an AC Power Switch inline is sufficient. Each machine will also need a Core, so we can read the ID of the user sewing.

### Circuitry

All electrical circuitry in MakeACS is designed to be easy to order, with BOM and Gerber files being optimized for use by JLCPCB and similar assembly houses. Further savings can be realized by doing partial or full assembly yourself. 

If we assume worst-case and have boards 100% assembled and shipped to us;

* 5x AC Power Switch: $324
* 5x NFC Core: $356
* International Shipping, Customs and Duties: $65

**Electronics Total: $745 (149 per machine)**

### Wiring

MakeACS uses standard HD15 cables to interconnect components. The suggested cable is one made by Amphenol Cables on Demand, but any quality brand should work. In our case, we'll opt for 5-foot cables, so we can mount the AC Power Switch out of the way, while still having the card reader easily accessed by the user.

* 5x Amphenol Cables on Demand HD15 5' (CS-DSDHD15MM0-005): $80.30
* Digikey Shipping & Tariffs: $64.08

The AC Power Switch also needs a cable to connect to the wall power. Any generic C13 (computer) power cable will work, but a 14AWG one rated for 15A is suggested to cover all load-cases.

* 5x 14AWG C13 Power Cable (Generic, Amazon): $60

**Wiring Total: $204.38 (40.88 per machine)**

### Enclosures

All MakeACS hardware enclosures are optimized for 3D printing, and can be printed on any printer you already own to save money! Alternatively there are no strict design specifications, so getting the manufactured externally would be inexpensive. 

For the AC Power Switch, it is suggested to use a UL94-V0 rated filament, to add an extra layer of thermal protection surrounding the electronics.

All 3D printed components for 5 AC Power Switches and 5 NFC Cores cost less than **$30** if you have your own 3D printer.

### Mechanical Hardware

MakeACS standardizes around very common metric M3 and M4 hardware, that can be bought in inexpensive bulk packs from Amazon, McMaster-Carr, or your local hardware store. This brings the hardware cost to only **$10** for our example.

The one somewhat specialized mechanical component needed would be the DIN rail mounting plate the NFC Core uses to attach itself to its base, a DRB48-1. A 5-pack of these is only **$15** on Amazon, though.

### Miscellaneous

Some other small miscellaneous things will be needed;

* 2A and 20A glass fuse for AC Power Switch: $2
* Dual-Lock or similar to mount the NFC Core and AC Power Switch: $5
* A USB-B cable for configuring the NFC Core (if you do not already have one): $5

### Total

Adding up the above, the total cost to deploy MakeACS hardware on 5 machines is only **$203 per machine**

The best part? It gets cheaper the more you buy, with bulk discounts especially present on the electronics. If we opted for 30 sets of hardware instead, it drops the price to under **$130 per machine**!

Adding additional features is also cheap and easy. For instance, adding a display to the Core is only $30 per unit more. Such upgrades can also come down the road thanks to the modular nature of the MakeACS hardware, so there's no need to make the decision right away.

## Server Cost

What good is the hardware being cheap if it costs a ton to keep the server running? The MakeACS server is designed to be extremely resource-conscious, requiring very little to run. We wouldn't recommend it, but you can easily run it off of a Raspberry Pi tucked away in the corner of the shop!

In most cases, hosting through a vendor like Heroku is the best option. Below is the configuration used by RIT, supporting over 8000 users across 7 makerspaces;

* Dyno (Heroku Cedar Basic): $7 per month: THe "computer" part of the server, that handles actually running the website.
* Datastore (Heroku Postgresql Essential 2), $20 per month: Handles database storage of all information. This plan allows full data logging for **50 years** before database size constraints kick in.
    * For smaller facilities, or if you can delete dater after ~5 years, you can get away with plans as little as $5 per month!

Some additional costs come into play if your scale gets very large;

* AWS Cloudfront CDN: Handles storing and serving images, documents, videos, etc. embedded into the website. Kept separate from Heroku to save costs. $0 per month unless you are exceeding around 10,000 website sessions per month. Beyond that, it costs around $1 per 100,000 monthly visits to the website.
* Mailgun: The part of Heroku that handles sending emails. Free for up to 400 emails per day, 401-50,000 emails per day costs up to $19 per month. Emails can be batched and sent out over time to keep under the 400 email limit, to avoid paying for the mail services.
* Grafana Hosting: If you want to use Grafana for visualizations, but do not want to have to host it yourself, you can integrate it into Heroku via Stackero for up to $19 per month.

So for most applications, the cost ends up **below $30 per month**!

Keep in mind: MakeACS is open-source. If your facility or institution already have server hosting capacity, you may be able to run MakeACS off of that for $0 per month!  