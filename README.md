# SenseMe
Python Library for Haiku SenseMe app controlled fans/lights

This library is useful to control Haiku SenseMe fans with light kits. I would expect it will probably also work with their lights.

It might also be useful for controlling DIY projects as the protocol is very simple and would be easy to clone. And, if you were to use their API the Android and iOS apps may work to control DIY devices. A suggested idea would be to add an Arduino or Raspberry Pi and a relay or two to your own fan and use this or the Haiku Home app to control them. I've read that doing this sort of thing [with a resistor is a dangerous idea, so don't do that.](https://arstechnica.com/civis/viewtopic.php?t=1263401)

Sample usage is found in [examples](tree/master/examples) and below.

Going forward, I expect to work this in with Flask to put on a VM to control the fan from a webpage on my phone or desktop. 

Sniffing the packets and documenting the protocol were the work of [Bruce](http://bruce.pennypacker.org/tag/senseme-plugin/). Much of the code was based on his work on making [an Indigo plugin](https://github.com/bpennypacker/SenseME-Indigo-Plugin)

See [Issues](issues) for known issues or if you want to contribute but don't know where to start.

I am not affiliated with Haiku Home or Big Ass Fans. Their support rep said this project seemed cool in it's infancy, and they even answered a technical question regarding the protocol for me, so hopefully they still approve.

# Future
Some ideas for future related projects and features:

 1. Plex plugin (dim the fans when the movie starts and light up when it is paused or ends? Yes, please!) [DCplaya has made some effort toward this.](https://github.com/dcplaya/SenseMe-Web-App)

 2. Alexa / Google Home plugins

 3. Store information in a database (sqlite would be fine) rather than discovering each time.

 4. Track usage and temperatures

 5. Other automation system plugins

 6. Real attempt at a Flask app with embeddable page for a dashboard system.

 7. Use protocol to control other devices by attaching an Arduino or Pi

 8. Discover the rest of the protocol. (Run strings on the apps and some packet sniffing.)

 9. More examples


## Usage
    from senseme import discover


    def main():
        # discover devices, returns list of SenseMe devices
        devices = discover()
        fan = devices[0]

        # Statically assign the fan? Probably not, but you would do it this way:
        # from senseme import SenseMe
        # fan = SenseMe('192.168.1.50', 'Living Room Fan', model='FAN')
        # fan = SenseMe(name="Living Room Fan")

        # Turn the light off / on
        # fan.light_powered_on = False
        # fan.light_powered_on = True
        # light_status = fan.light_toggle()

        # Increase light level by 2 levels
        # fan.inc_brightness(2)

        # Get Light level
        # print(fan.brightness)

        # Fan Speeds
        # fan.fan_powered_on = True
        # fan.fan_powered_on = False
        # print(fan.speed)
        # fan.speed = 5

        # whoosh mode
        # fan.whoosh = True

        # want an increasing light effect? Do this.
        # But, really, probably don't, I don't think Haiku intended strobe effects.
        # I'm not responsible if you make a strobe light and break the fan or worse
        # for intensity in range(1,16):
        #   fan.brightness = intensity
        #   time.sleep(1)

        # export details to json / xml / str(dict)
        # fan.json
        # fan.xml
        # fan.dict  # nested dict
        # fan.flat_dict  # flattened

        # Listen for broadcasts, useful for debugging,
        # wouldn't suggest using it for anything else
        # fan.listen()


    main()
